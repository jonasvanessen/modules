The main reason to use a VLAN is to mitigate all the broadcast messages, which could consist of:
Also a reason is, that it is very scalable, since you don't need new equipment.

ARP (Address Resolution Protocol) Requests:

Devices use ARP to discover the MAC address associated with a given IP address. ARP requests are broadcast messages.
DHCP (Dynamic Host Configuration Protocol) Requests:

When a device joins a network and needs an IP address, it sends out a DHCP request, which is typically broadcast to the entire local network.
NetBIOS Name Service:

NetBIOS (Network Basic Input/Output System) uses broadcast messages to resolve NetBIOS names to IP addresses.
Link Layer Discovery Protocol (LLDP):

Used by network devices to advertise their identity and capabilities to neighboring devices. LLDP messages are typically broadcast.
IPv6 Neighbor Discovery:

Similar to ARP in IPv4, Neighbor Discovery in IPv6 uses broadcast-like messages to resolve IP addresses to link-layer addresses.
Router Advertisements:

In IPv6, routers periodically send router advertisements to announce their presence and provide network configuration information. These messages can be broadcast.
Layer 2 (Switch) Broadcasts:

Various Layer 2 protocols use broadcast messages for tasks like spanning tree protocol (STP) to prevent loops in the network.


## Trunk Ports
https://www.youtube.com/watch?v=A9lMH0ye1HU&list=RDCMUCZg4PvX48mgXQVySgIulX-Q&index=3

Used to send traffic from one network to another.
To identify, from which vlan traffic was sent from, we need to use something called a tag.
802.1Q (Dot-1Q) Tag will be added to the data package when going from one switch to another.
