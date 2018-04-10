
Computers are hard.

<!-- TODO
State machine of a placement.

Document versioning.

Serialization framework. Versioning. API versioning. Storage system.
-->

---

### Networking

I've got an application running inside a container within Docker on
my Mac, inside a virtual machine (VM). There's another app in the cloud,
also containerized, maybe in a VM. What does communication look like
between them?

Does the remote machine have single-route IO virtualization (SR/IOV)
enabled? How about VirtIO? Is the cloud running a network overlay? 
Is it VxLAN?
Multi-packet label switching (MPLS)? General routing encapsulation
(GRE)? Is there a smart NIC with full OVS offload? Did we install the
right kernel drivers? 

Is Docker running in NAT or bridge mode? Why are DNS lookups failing?
Am I running DnsMasq? Why is the DHCP range misconfigured? Are the
containers using IpVlan or MacVlan? Or maybe a veth pair? Is my
iptables config correct?

Is my traffic going over the VPN? What's wrong with the split tunnel?
Is the configured web proxy interfering? Have I configured it in all
the right places? Host OS, guest OS, container, Docker daemon? Is my
Yubikey properly configured?

Are the firewall rules correct? On my local machine? In the cloud
networking config? In Kubernetes? Is there a load balancer configured?
Does this cloud let me share a subnet across availability zones? What
about portable IPs? Will GARP (gratuitous address resolution protocol)
work in this environment? For my app to be high availability do I need
multiple subnets? Do I need to configure different virtual private
clouds (VPCs) for dev and prod?

How does my app access cloud infrastructure services? How do I get the
relevant credentials to them? Is there a pre-installed machine cert that
will help me bootstrap? What's the PKI story, and how do we do key
rotation? Does the smartNIC need to be configured to talk across VPCs?
Or do we configure a load balancer at the border and require tromboning?

So when someone comes up and asks me "hey, I'm having trouble connecting
to the app," my mind has to switch from whatever it's doing to swimming
through dozens of intersecting degrees of complexity to even begin to
think about the question. I *think* an SSH reverse tunnel will help,
but I have to painfully plod through the reasoning to make sure I'm
not saying something that makes absolutely no sense.

> Just connect this nerve to that capillary.

Dude, those aren't even the same kind of thing. What kind of doctor
did you say you were?

---

### Programming

Learning a new language is hard.

You'll be passed a function which takes an authentication request
header, and must return a future of either a result, or else a flow
(of generic In/Out types), which must come with an implicit transformer,
and return a websocket.

```scala
  def acceptOrResult[In, Out](f: AuthNRequestHeader => Future[Either[Result, Flow[In, Out, _]]])(implicit transformer: MessageFlowTransformer[In, Out]): WebSocket =
  WebSocket.acceptOrResult { request =>
    val cmdId = extractCmdId(request)

    val result = for {
      authnRequestHeader <- authN.authenticate(cmdId, request).map(AuthNRequestHeader(_, cmdId, request)).leftMap(handleAuthError)
      flow <- EitherT(f(authnRequestHeader))
    } yield flow
    result.value
  }

```

Don't forget that this all has to be appropriately backpressured. And
we're using Actors. For that, you'll need to write something like this:

```scala
    def actorRefFlow[In, Out](propsFunc: (WebsocketContext[In, Out]) => Props, inBufSz: Int = 256, outBufSz: Int = 256)
                             (implicit actorSystem: ActorRefFactory) = {
      implicit val ec = actorSystem.dispatcher

      Flow
        .fromSinkAndSourceMat(
          Sink.asPublisher[In](fanout = false),
          Source.asSubscriber[Out])(Keep.both)
        .viaMat(KillSwitches.single[Out])((t, ks) => WebsocketContext(t._1, t._2, killSwitchAsPromise(ks)))
        .mapMaterializedValue { ctx =>
          actorSystem.actorOf(propsFunc(ctx))
          NotUsed
        }
        .join(Flows.mutualCompleter[In, Out])
    }
```

Are you sure the KillSwitch and MutualCompleter are connected in such
a way that when the client closes the Websocket, your Flow finishes as
well?

As it turns out, there's a bug in your json parser which quietly
gets [swallowed by the framework](https://groups.google.com/forum/#!searchin/play-framework/aditya$20prasad%7Csort:date/play-framework/rtN1G2eRyGA/aGX_Et78DgAJ).

Once you get through that, you discover a bug in the library: you have
a websocket client writing to and reading from the above server. If your
reading side terminates, the writing side should finish too:

> "The Akka HTTP WebSocket API does not support half-closed connections which means that if the either stream completes the entire connection is closed."

But it's not. And when you reach out to the mailing list, you get an
[RTFM](https://groups.google.com/d/msg/akka-user/Bl4l0YsbkDE/uOmKmQ4UBwAJ).
So you file a bug and discover that [nobody's quite sure](https://github.com/akka/akka/issues/21089#issuecomment-238182023) whether it's a bug
or a documentation issue.

So now you have to roll your own solution for killing on side of a Flow
when the other side terminates:

{: style="overflow:scroll; height:300px;"}
```scala
def fromSinkAndSource[I, O](sink: Graph[SinkShape[I], _], source: Graph[SourceShape[O], _]): Flow[I, O, Unit] = {
  val p1 = Promise[Unit]()
  val p2 = Promise[Unit]()
  val tw1 = tw[I](p1.complete, p2)
  val tw2 = tw[O](p2.complete, p1)
  tw1.via(Flow.fromSinkAndSource(sink, source)).via(tw2)
}

abstract class KillableGraphStageLogic(val terminationSignal: Future[Unit], _shape: Shape) extends GraphStageLogic(_shape) {
  override def preStart(): Unit = {
    terminationSignal.value match {
      case Some(status) ⇒ onSwitch(status)
      case _ ⇒ terminationSignal.onComplete(getAsyncCallback[Try[Unit]](onSwitch).invoke)
    }
  }

  private def onSwitch(mode: Try[Unit]): Unit = mode match {
    case Success(_)  ⇒ completeStage()
    case Failure(ex) ⇒ failStage(ex)
  }
}

case class TerminationWatcher(callback: Try[Unit] ⇒ Any, promise: Promise[Unit]) extends GraphStageWithMaterializedValue[FlowShape[Any, Any], Unit] {
  val in = Inlet[Any]("terminationWatcher.in")
  val out = Outlet[Any]("terminationWatcher.out")
  override val shape = FlowShape(in, out)

  override def createLogicAndMaterializedValue(attr: Attributes) = {
    val logic = new KillableGraphStageLogic(promise.future, shape) {
      setHandler(in, new InHandler {
        override def onPush(): Unit = push(out, grab(in))

        override def onUpstreamFinish(): Unit = {
          callback(Success[Unit](()))
          completeStage()
        }

        override def onUpstreamFailure(ex: Throwable): Unit = {
          callback(Failure(ex))
          failStage(ex)
        }
      })

      setHandler(out, new OutHandler {
        override def onPull(): Unit = pull(in)

        override def onDownstreamFinish(): Unit = {
          callback(Success[Unit](()))
          completeStage()
        }
      })
    }
    (logic, ())
  }

  override def toString = "TerminationWatcher"
}

def terminationWatcher[T](callback: Try[Unit] => Any, promise: Promise[Unit]): GraphStageWithMaterializedValue[FlowShape[T, T], Unit] =
  TerminationWatcher(callback, promise).asInstanceOf[GraphStageWithMaterializedValue[FlowShape[T, T], Unit]]

def tw[T](callback: Try[Unit] => Any, promise: Promise[Unit]) = Flow.fromGraph(terminationWatcher[T](callback, promise))
```

It turns out there's a simpler way to implement this, but it seems I had to
first pay my dues before finding it.

After a few months of this you discover that your *real* problem is that 
the two main abstractions of the library (Streams and Actors) are
not really meant to be used together:

> "Sink.actorRef corresponds to leaving the end of the hose open and unconnected, placing a bucket below it that will hopefully catch most of the water.

> So, to conclude: if you want to use our nice and watertight websockets, then you’ll have to use hoses (Streams) and not hammers (Actors). Of course you can use a hammer to build a “hose” but that will be a lot of work since you’ll effectively be smithing a manifold."

In other words, your whole system is built on a leaky abstraction. Good
luck!

---

### Authentication and authorization

A company using our cloud has lots of users. Some users are administrators,
able to setup identity and access management (IAM) settings for the rest. The 
cloud has its own IAM system. Users can be assigned roles; users and/or roles
can belong to security compartments. Compartments determine how resources can
be allocated.

Should we use their IAM model for access to our service? What if it changes out
from under us? Should we instead use the cloud's IAM for identity and then
manage access (authorization) ourselves? That seems easiest.

Users can write their own schedulers for use with their application. We have to
deploy their schedulers (and ensure that exactly one is running). How does this
(containerized) process get credentials for our service?

When one of their machines starts up and runs our agent, how does that agent
communicate with our service? Where do its credentials come from? If the
process is one-click for them to start up an instance with our agent, does that
process look different than if they deploy our agent themselves on existing
hardware?

When the user requests a new instance running our agent, we have to generate
a temporary secret (maintained by our service) that we feed as metadata to
the instance requisitioning service.

---

What is the bootup story for the box? I think it's using iSCSI with
PCI-passthrough of virtual functions. Since I'm using KVM maybe I should
use iPXE? Where does UEFI fit in?

> I have build snponly.efi, which can run in my UEFI uut, but when I
want to use sanboot cmd to connect my iscsi target server, nothing
happened. … I notice that the iscsi operation will call int13 api in
/arch/i386/interface/pcbios/int13.c at legacy BIOS version.

---

Maybe I should just roll up my sleeves and start trying things out?
I have to install a package, but I'm using different flavors of Linux
in different places. Is this one DEB or RPM? Crap, it's the wrong one.
Should I use Alien to convert? What are these nonsense errors it's
spitting out? Maybe I should just build a CentOS image myself. It
works, but

`Docker Failed to get D-Bus connection: Operation not permitted`

What? Oh, obviously I have to add these flags to the Docker command:

`--privileged -ti -e "container=docker"  -v /sys/fs/cgroup:/sys/fs/cgroup`

I finally get it working! -- only to realize that Java is not installed.
Here's more fun journaling from that day:

> Bob suggests building a RHEL container that has Java. That fails
because Docker daemon copies my /etc/resolv.conf into the container,
which points at 127.0.0.1 because dnsmasq is being too clever. I try
to remove dnsmasq but it tries to remove ubuntu-desktop. So I discover
that I must edit /lib/systemd/system/docker.service to pass a DNS server
that Tony reads out to me.

But I'm actually running on a Macintosh, so I need to do this all
inside a Linux container inside a VM.

---

<!--
TODO

Whitebox switch
Off-the-shelf components
DPDK
VirtIO


-->



