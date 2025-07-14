#Written for Cisco 2960. Some cisco commands may vary.

# Basic Config
```
!
hostname CISCO_Switch_2960
logging userinfo
logging buffered 5000 informational
logging console informational
logging monitor informational
enable secret 9 <secure_password>
enable password 7 <enable_password>
!
username admin privilege 15 password 7
aaa new-model
aaa local authentication default authorization default
aaa authorization exec default local
aaa authorization network default local
!
!
!
!
!
!
!
aaa session-id common
clock timezone UTC 0
clock summer-time UTC recurring
system mtu routing 1500
!
!
!
!
ip routing
no ip gratuitous-arps
ip dhcp bootp ignore
!
!
ip dhcp snooping vlan <vlan#s>
ip dhcp snooping
no ip domain-lookup
ip domain-name domain.local
login block-for 900 attempts 3 within 120
login on-failure log
login on-success log
vtp mode off
!
! Configure the VLANs
interface vlan 10
description Management
ip address 10.10.10.10 255.255.255.0
no shutdown
!
interface vlan 20
description Data
no shutdown
!
interface vlan 30
description Voice
no shutdown
!
interface FastEthernet0/1
 description Uplink to Router
 switchport mode trunk
 switchport trunk allowed vlan 10,20,30
 no shutdown
 !
interface FastEthernet0/2-5
 description Access Ports
 switchport mode access
 switchport access vlan 20
 no shutdown
!
interface FastEthernet0/6-10
 description Voice Ports
 switchport mode access
 switchport access vlan 30
 no shutdown
!
interface FastEthernet0/11-24
 description Unused Ports
 shutdown
 exit
!
ip ssh time-out 60
ip ssh version 2
!
banner login ^CI've read & consent to terms in IS user agreement
^C
!
line vty 0 1
 access-class MGT in
 transport preferred ssh
 transport input ssh
!
end
```

# Config with notes
```
#enter switch
    en
#configure switch mode
    conf t
#set hostname of switch
    hostname CISCO_Switch_hostname

```
