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
```












```

```
