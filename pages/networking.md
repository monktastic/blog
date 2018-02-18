

I've got an application running inside a container within Docker on
my Mac, inside a VM. There's another app in the cloud, also
containerized, maybe in a VM. What does communication look like between
them?

Does the remote machine have SR/IOV enabled? Is the cloud running a
network overlay? Is it VxLAN? MPLS over GRE? Is there a smart NIC
with full OVS offload? Did I install the right kernel drivers? How about
virtIO? Is my iptables config correct?

Is Docker running in NAT or bridge mode? Why are DNS lookups failing?
Am I running DnsMasq? Why is the DHCP range misconfigured? Are the
containers using IpVlan or MacVlan? Or maybe just a veth pair?

Is my traffic going over the VPN? What's wrong with the split tunnel?
Is the configured web proxy interfering? Have I configured it in all
the right places? Host OS, guest OS, container, Docker daemon? Is my
Yubikey properly configured?

Are the firewall rules correct? On my local machine? In the cloud
networking config? In Kubernetes? Is there a load balancer configured?
Does the cloud let me share a subnet across availability zones? What
about portable IPs? For my app to be high availability do I need
multiple subnets? Do I need to configure different VPCs for dev and
prod?

How does my app access cloud services? How do I get the relevant
credentials to it? Is there a pre-installed machine cert that will help
me bootstrap? What's the PKI story, and how do we do key rotation?
Does the smartNIC need to be configured to talk across VPCs? Or do
we configure a load balancer at the border and require tromboning?

What is the bootup story for my box? I think it's using iSCSI with
PCI-passthrough of virtual functions. Since I'm using KVM maybe I should
use iPXE? Where does UEFI fit in?

> I have build snponly.efi, which can run in my UEFI uut, but when I
want to use sanboot cmd to connect my iscsi target server, nothing
happened. … I notice that the iscsi operation will call int13 api in
/arch/i386/interface/pcbios/int13.c at legacy BIOS version.

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





