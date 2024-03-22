# GNS3

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

# Einen Port (Only Untagged) zu einer Bridge hinzufügen (z.B. für ein Endgerät)
/interface/bridge/port add bridge=my-bridge comment="VLAN [101]  [Zimmer1]" frame-types=admit-only-untagged-and-priority-tagged hw=no interface=ether1 pvid=101
/interface/bridge/port add bridge=my-bridge comment="VLAN [101]  [Zimmer1]" frame-types=admit-only-untagged-and-priority-tagged hw=no interface=ether2 pvid=101

# Ein VLAN einer Bridge hinzufügen, sowie «tagged» und «untagged» ports definieren (hier nur untagged)
/interface/bridge/vlan add bridge=my-bridge comment="VLAN [101]" untagged=ether1,ether2 vlan-ids=101

# Bridge information anschauen
/interface/bridge/vlan print
/interface/bridge/port print
´´´