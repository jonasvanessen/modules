# VLAN

## Basics

By default, all interfaces are assigned to VLAN 1.

List VLANS
```
S2# show vlan brief
```


Create the following VLANs. Names are case-sensitive and must match the requirement exactly:
```
S1#(config)# vlan 10
S1#(config-vlan)# name Faculty/Staff
```

Which command will only display the VLAN name, status, and associated ports on a switch
```
S2>show vlan brief
```

ACCESS PORTS
```
S2(config)# interface f0/11
S2(config-if)# switchport mode access
S2(config-if)# switchport access vlan 10
```

TRUNKING
```
S1(config)# interface range g0/1 - 2
S1(config-if)# switchport mode trunk

# Configure VLAN 99 as the native VLAN for G0/1 and G0/2 interfaces on S1.
S1(config-if)# switchport trunk native vlan 99
```

command to verify the correct native VLAN configuration.
```
show interface trunk
```

set ip address for vlan on switch
```
interface vlan 99
ip address 192.168.99.253 255.255.255.0
```
















