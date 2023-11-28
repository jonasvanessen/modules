# Cisco Packet Tracer Intro


## Basic Device setup

* Add Clients
* Add Switch: 2960-24TT
* Add Router: 2811
* Use Copper to connect Clients and Switch (Fa0, Fa0/1)
* Use Copper to connect Clients and Switch (Fa0, Fa0/2)

## Configuration

### Set up router for dhcp

On the router, configure interface fa0/0 to act as the default gateway for our LAN.

```
Router>enable
Router#config terminal
Router(config)#int fa0/0
Router(config-if)#ip add 192.168.0.1 255.255.255.0
Router(config-if)#no shutdown
Router(config-if)#exit
```

Configure DHCP server on the Router. In the server we will define a DHCP pool of IP addresses to be assigned to hosts, a Default gateway  for the LAN and a DNS Server (optional).

```
Router(config)#
Router(config)#ip dhcp pool net1
Router(dhcp-config)#network 192.168.0.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.0.1
Router(dhcp-config)#exit
Router(config)#

Router(config)#
Router(config)#ip dhcp pool net2
Router(dhcp-config)#network 192.168.1.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.1.1
Router(dhcp-config)#exit
Router(config)#
```

We can add ip dhcp excluded-address command to our configuration so as to configure the router to exclude addresses 192.168.0.1 through 192.168.0.10 when assigning addresses to clients:
```
Router(config)#ip dhcp excluded-address 192.168.1.1 192.168.1.10
```

### Client Setup

Click PC1->Desktop->IP configuration. Then enable DHCP:

![Alt text](image.png)


# Sources

* https://computernetworking747640215.wordpress.com/2018/07/05/how-to-configure-dhcp-server-in-packet-tracer/
* https://www.youtube.com/watch?v=dyVXVQgos4Q
