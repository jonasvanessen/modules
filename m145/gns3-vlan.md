# GNS3

## Links
* https://wiki.mikrotik.com/wiki/Manual:Interface/Bridge
  

## Clients

´´´
Edit config
ip address [mask] [gateway]
ip 192.168.1.20 255.255.255.0
´´´


## Routers

´´´
# Neue VLAN fähige Bridge hinzufügen
/interface/bridge add name=my-bridge protocol-mode=none vlan-filtering=yes
´´´

´´´
# Einen Port (Only Untagged) zu einer Bridge hinzufügen (z.B. für ein Endgerät)
/interface/bridge/port add bridge=my-bridge comment="VLAN [101]  [Zimmer1]" frame-types=admit-only-untagged-and-priority-tagged hw=no interface=ether1 pvid=101
/interface/bridge/port add bridge=my-bridge comment="VLAN [101]  [Zimmer1]" frame-types=admit-only-untagged-and-priority-tagged hw=no interface=ether2 pvid=101
´´´

´´´
# Anderes VLAN
/interface/bridge/port add bridge=my-bridge comment="VLAN [102]  [Zimmer1]" frame-types=admit-only-untagged-and-priority-tagged hw=no interface=ether3 pvid=102
/interface/bridge/port add bridge=my-bridge comment="VLAN [102]  [Zimmer1]" frame-types=admit-only-untagged-and-priority-tagged hw=no interface=ether4 pvid=102
´´´

´´´
# Ein VLAN einer Bridge hinzufügen, sowie «tagged» und «untagged» ports definieren (hier nur untagged)
/interface/bridge/vlan add bridge=my-bridge comment="VLAN [101]" untagged=ether1,ether2 vlan-ids=101
/interface/bridge/vlan add bridge=my-bridge comment="VLAN [102]" untagged=ether3,ether4 vlan-ids=102
´´´

´´´
# Bridge information anschauen
/interface/bridge/vlan print
/interface/bridge/port print
´´´
