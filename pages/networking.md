
My mind was rejecting the immense complexity of the project. It's hard
to summarize, because there are so many different dimensions to it.

---

### Networking

I've got an application running inside a container within Docker on
my Mac, inside a virtual machine (VM). There's another app in the cloud,
also containerized, maybe in a VM. What does communication look like
between them?

Does the remote machine have single-route IO virtualization (SR/IOV)
enabled? Is the cloud running a network overlay? Is it VxLAN?
Multi-packet label switching (MPLS) over general routing encapsulation
(GRE)? Is there a smart NIC with full OVS offload? Did we install the
right kernel drivers? How about virtIO?

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
are you?

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
we're using Actors. For that, you'll need to write something like an
ActorRefFlow.

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





