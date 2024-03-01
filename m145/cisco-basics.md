# Cisco Basics

# Part 1: Verify the Default Switch Configuration
## Step 1: Enter privileged EXEC mode.
You can access all switch commands from privileged EXEC mode. However, because many of the privileged commands configure operating parameters, privileged access should be password-protected to prevent unauthorized use.

The privileged EXEC command set includes the commands available in user EXEC mode, many additional commands, and the configure command through which access to the configuration modes is gained.

a.  Click S1 and then the CLI tab. Press Enter.

b.  Enter privileged EXEC mode by entering the enable command:

Open Configuration Window for S1

```
Switch> enable
Switch#
```

Notice that the prompt changed to reflect privileged EXEC mode.

## Step 2: Examine the current switch configuration.

```
Switch# show running-config
```
# Part 2: Create a Basic Switch Configuration

## Step 1: Assign a name to a switch.
To configure parameters on a switch, you may be required to move between various configuration modes. Notice how the prompt changes as you navigate through the switch.

```
Switch# configure terminal

Switch(config)# hostname S1

S1(config)# exit

S1#
```


## Step 2: Secure access to the console line.
To secure access to the console line, access config-line mode and set the console password to letmein.
```
S1# configure terminal

Enter configuration commands, one per line. End with CNTL/Z.

S1(config)# line console 0

S1(config-line)# password letmein

S1(config-line)# login

S1(config-line)# exit

S1(config)# exit

%SYS-5-CONFIG_I: Configured from console by console

S1#
```

## Step 3: Verify that console access is secured.
Exit privileged mode to verify that the console port password is in effect.
```
S1# exit

Switch con0 is now available

Press RETURN to get started.

 

User Access Verification

Password:

S1>
```
Note: If the switch did not prompt you for a password, then you did not configure the login parameter in Step 2.

## Step 4: Secure privileged mode access.
Set the enable password to c1$c0. This password protects access to privileged mode.

Note: The 0 in c1$c0 is a zero, not a capital O. This password will not grade as correct until after you encrypt it in Step 8.
```
S1> enable

S1# configure terminal

S1(config)# enable password c1$c0

S1(config)# exit

%SYS-5-CONFIG_I: Configured from console by console

S1#
```
## Step 5: Verify that privileged mode access is secure.
a.     Enter the exit command again to log out of the switch.

b.     Press <Enter> and you will now be asked for a password:
```
User Access Verification

Password:
```
c.     The first password is the console password you configured for line con 0. Enter this password to return to user EXEC mode.

d.     Enter the command to access privileged mode.

e.     Enter the second password you configured to protect privileged EXEC mode.

f.      Verify your configuration by examining the contents of the running-configuration file:
```
S1# show running-config
```

Notice that the console and enable passwords are both in plain text. This could pose a security risk if someone is looking over your shoulder or obtains access to config files stored in a backup location.

## Step 6: Configure an encrypted password to secure access to privileged mode.
The enable password should be replaced with the newer encrypted secret password using the enable secret command. Set the enable secret password to itsasecret.
```
S1# config t

S1(config)# enable secret itsasecret

S1(config)# exit

S1#
```
Note: The enable secret password overrides the enable password. If both are configured on the switch, you must enter the enable secret password to enter privileged EXEC mode.

## Step 7: Verify that the enable secret password is added to the configuration file.
Enter the show running-config command again to verify the new enable secret password is configured.

Note: You can abbreviate show running-config as
```
S1# show run
```
Questions:
What is displayed for the enable secret password?

Why is the enable secret password displayed differently from what we configured?

## Step 8: Encrypt the enable and console passwords.
As you noticed in Step 7, the enable secret password was encrypted, but the enable and console passwords were still in plain text. We will now encrypt these plain text passwords using the service password-encryption command.
```
S1# config t

S1(config)# service password-encryption

S1(config)# exit
```
Question:
If you configure any more passwords on the switch, will they be displayed in the configuration file as plain text or in encrypted form? Explain


# Part 3: Configure a MOTD Banner
## Step 1: Configure a message of the day (MOTD) banner.
The Cisco IOS command set includes a feature that allows you to configure messages that anyone logging onto the switch sees. These messages are called message of the day, or MOTD banners. Enclose the banner text in quotations or use a delimiter different from any character appearing in the MOTD string.
```
S1# config t

S1(config)# banner motd "This is a secure system. Authorized Access Only!"

S1(config)# exit

%SYS-5-CONFIG_I: Configured from console by console

S1#
```
Questions:
When will this banner be displayed?

Why should every switch have a MOTD banner?

## Part 4: Save and Verify Configuration Files to NVRAM
Step 1: Verify that the configuration is accurate using the show run command.
Save the configuration file. You have completed the basic configuration of the switch. Now back up the running configuration file to NVRAM to ensure that the changes made are not lost if the system is rebooted or loses power.
```
S1# copy running-config startup-config

Destination filename [startup-config]?[Enter]

Building configuration...

[OK]

Close Configuration Window for S1
```
Questions:
What is the shortest, abbreviated version of the copy running-config startup-config command?

Examine the startup configuration file.

Which command will display the contents of NVRAM?

Are all the changes that were entered recorded in the file?


# Part 3: Configure the Switch Management Interface
Configure S1 and S2 with an IP address.

## Step 1: Configure S1 with an IP address.
Switches can be used as plug-and-play devices. This means that they do not need to be configured for them to work. Switches forward information from one port to another based on MAC addresses.

Question:
If this is the case, why would we configure it with an IP address?

Answer: VLAN Configuration: While basic switching operations rely on MAC addresses, advanced features such as VLANs (Virtual Local Area Networks) often require IP connectivity for management and configuration.

And more: Monitoring and Logging, Remote Management, Quality of Service (QoS) Configuration

Use the following commands to configure S1 with an IP address.
```
S1# configure terminal

Enter configuration commands, one per line. End with CNTL/Z.

S1(config)# interface vlan 1

S1(config-if)# ip address 192.168.1.253 255.255.255.0

S1(config-if)# no shutdown

%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan1, changed state to up

S1(config-if)#

S1(config-if)# exit

S1#
```
Question:
Why do you enter the no shutdown command?

Answer: In the simplest sense, shutdown turns the interface off. no shutdown turns the interface on (enables it).

### Default Gateway

Sometimes gateway is needed:
```
LAN-A(config)#ip default-gateway 192.168.0.63
```

### Configure router

```
CustomerRouter(config)#interface g0/1
CustomerRouter(config-if)#ip address 192.168.0.65
% Incomplete command.
CustomerRouter(config-if)#ip address 192.168.0.65 255.255.255.192
CustomerRouter(config-if)#no shutdown
```


## Step 3: Verify the IP address configuration on S1 and S2.
Use the show ip interface brief command to display the IP address and status of all the switch ports and interfaces. You can also use the show running-config command.

```
S1#show ip interface brief

or...

S1#show ip interface brief
```

## Step 4: Save configurations for S1 and S2 to NVRAM.

```
S1# copy running-config startup-config

Destination filename [startup-config]?[Enter]

Building configuration...

[OK]

Close Configuration Window for S1
```
# ARP Request

Enter the arp -d command to clear the ARP table.

Clear arp table
```
arp -d
```
List
```
arp -a 
```

Show arp table on a switch
```
Switch>show mac-address-table

          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----

   1    0002.1640.8d75    DYNAMIC     Fa0/3
   1    000c.85cc.1da7    DYNAMIC     Fa0/1
   1    0060.7036.2849    DYNAMIC     Fa0/2
   1    00e0.f7b1.8901    DYNAMIC     Gig0/1
```

On a Router

```
Router>enable

Router#show mac-address-table

          Mac Address Table
-------------------------------------------

Vlan    Mac Address       Type        Ports
----    -----------       --------    -----


Router#show arp


Protocol  Address          Age (min)  Hardware Addr   Type   Interface
Internet  172.16.31.1             -   00E0.F7B1.8901  ARPA   GigabitEthernet0/0
Internet  172.16.31.2             1   000C.85CC.1DA7  ARPA   GigabitEthernet0/0
```

# Subnetting

(/25) 11111111.11111111.11111111.10000000

Dotted decimal subnet mask equivalent:

Number of subnets? Number of hosts?
```
Anzahl Subnetze: Number of Subnets=2^(CIDR - Total bits in network portion)
2^(25-24) = 2

Bei /18
2^(18-16) = 4


Anzahl möglicher Hosts bestimmen: 2^(32-CIDR) -2 = Anzahl Hosts

2^(32-25)-2 = 126
```

(/29) 11111111.11111111.11111111.11111000

Dotted decimal subnet mask equivalent:

Number of subnets? Number of hosts?

```
Anzahl Subnetze: Number of Subnets=2^(CIDR - Total bits in network portion)
2^(29-24) = 32

Anzahl möglicher Hosts bestimmen: 2^(32-CIDR) -2 = Anzahl Hosts

2^(32-29)-2 = 6
```
## IPv4 - Netz-, Broadcast-, und Host-Adressen bestimmen

```
# Schritt 1: IPv4 Adresse in binäre Form umwandeln
Address:   192.168.6.4          11000000.10101000.00000110. 00000100

# Schritt 2: Netzmaske und Wildcard in binäre Form umwandeln
Netmask:   255.255.255.0 = 24   11111111.11111111.11111111. 00000000
                                <=        24 Eins       =>
Wildcard:  0.0.0.255            00000000.00000000.00000000. 11111111
                                                            <8 Eins>
                                24 Bits + 8 Bits = 32 Bits = 4 Bytes

# Schritt 3: Logisch UND (&) mit der IPv4-Adresse & Netzmaske ergibt Netzadresse
Address:   192.168.6.4          11000000.10101000.00000110. 00000100
 & Netmask:   255.255.255.0     11111111.11111111.11111111. 00000000
 = Network:   192.168.6.0/24    11000000.10101000.00000110. 00000000

# Schritt 4: Netzmaske + 1 ergibt HostMin
Network:   192.168.6.0/24       11000000.10101000.00000110. 00000000
+ 1                             00000000.00000000.00000000. 00000001
= HostMin:   192.168.6.1          11000000.10101000.00000110. 00000001

# Schritt 5: Netzmaske & Wildcard = Broadcast
Network:   192.168.6.0/24       11000000.10101000.00000110. 00000000
& Wildcard                      00000000.00000000.00000000. 11111111
 = Broadcast: 192.168.6.255     11000000.10101000.00000110. 11111111

# Schritt 6: Broadcast - 1 ergibt HostMax
Broadcast: 192.168.6.255     11000000.10101000.00000110. 11111111
 -1                          00000000.00000000.00000000. 00000001
 = HostMax: 192.168.6.254    11000000.10101000.00000110. 11111110

# Schritt 7: Anzahl möglicher Hosts bestimmen: 2^(32-CIDR) -2 = Anzahl Hosts
2^(32-24) - 2 = 254
```

=======


# Router
From SNMP exercise
```
Router>enable
Router#config t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#interface g0/0
Router(config-if)#ip address 192.168.2.1 255.255.255.0
Router(config-if)#no shutdown
Router(config-if)#
```

SNMP, [source](https://www.cisco.com/c/en/us/support/docs/ip/simple-network-management-protocol-snmp/7282-12.html) 
```
Router>enable
Router#config t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#snmp-server community M145pub RO
%SNMP-5-WARMSTART: SNMP agent on host Router is undergoing a warm start
Router(config)#snmp-server community M145pri RW
Router(config)#exit
Router#
%SYS-5-CONFIG_I: Configured from console by console
copy run start
Destination filename [startup-config]? 
Building configuration...
[OK]
Router#
Router#show running-config 
.... 
.... 
snmp-server community public RO 
snmp-server community private RW 
.... 
....
```
