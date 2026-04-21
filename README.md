# VlanRouting

Virtual Trunking Protocol & Intervlan Routing

In this lab I set up VLAN VTP and configure intervlan routing on multiple switches

 <img width="991" height="431" alt="image" src="https://github.com/user-attachments/assets/21370766-2e7d-4a10-a622-a34a6d428573" />


Switch Configurations then using the sh vlan command to display information

Mainswitch Configurations 
en
config t
vlan 10 
name student
vlan 20
name faculty
int vlan 20
ip add 150.10.64.250 255.255.224.0
no shut
int range f0/5-8
switchport mode access
swtichport access vlan 10
int range f0/9-12
switchport mode access
swtichport access vlan 20
int range f0/23-24, g0/1
switchport mode trunk
end
config t
vtp mode server
ip default-gateway 150.10.95.254
ip domain-name cisco.com
crypto key gen rsa
1024
username admin secret cisco
ip ssh ver 2
line vty 0
login local
transport input ssh
end
copy run start

 <img width="856" height="708" alt="image" src="https://github.com/user-attachments/assets/5fff38f8-9992-4f1e-b121-53063b9c1202" />


SwitchB Configurations 
en
config t
vlan 10 
name student
vlan 20
name faculty
int vlan 20
ip add 150.10.64.50 255.255.224.0
no shut
int range f0/5-8
switchport mode access
swtichport access vlan 10
int range f0/9-12
switchport mode access
swtichport access vlan 20
int range f0/2-3
switchport mode access
switchport port-security max 1
switchport port-security mac-address sticky
switchport port-security vio shutdown
exit
int range f0/23-24
switchport mode trunk
end
config t
vtp mode client
ip default-gateway 150.10.95.254
ip domain-name cisco.com
crypto key gen rsa
1024
username admin secret cisco
ip ssh ver 2
line vty 0
login local
transport input ssh
end
copy run start
 

<img width="682" height="578" alt="image" src="https://github.com/user-attachments/assets/f9ec6c06-0f17-4b22-b60a-bece2c2f5977" />

SwitchC Configurations
en
config t
vlan 10 
name student
vlan 20
name faculty
int vlan 20
ip add 150.10.64.150 255.255.224.0
no shut
int range f0/5-8
switchport mode access
swtichport access vlan 10
int range f0/9-12
switchport mode access
swtichport access vlan 20
int range f0/2-3
switchport mode access
switchport port-security max 1
switchport port-security mac-address sticky
switchport port-security vio shutdown
exit
int range f0/23-24
switchport mode trunk
end
config t
vtp mode client
ip default-gateway 150.10.95.254
ip domain-name cisco.com
crypto key gen rsa
1024
username admin secret cisco
ip ssh ver 2
line vty 0
login local
transport input ssh
end
copy run start

<img width="644" height="573" alt="image" src="https://github.com/user-attachments/assets/4862a8fc-34dc-4081-a6e1-f5b3a97a72fa" />
 

Router Configurations 
en
config t
int g0/1
no shut
int g0/1.1
encapsulation dot1q 1
ip add 150.10.31.254 255.255.224.0 
int g0/1.10
encapsulation dot1q 10
ip add 150.10.63.254 255.255.224.0 
int g0/1.20
encapsulation dot1q 20
ip add 150.10.95.254 255.255.224.0
end
copy run start


Ip Interface Brief 

Here I would display information about the router and switches using the sh ip int brief command

Router

<img width="740" height="242" alt="image" src="https://github.com/user-attachments/assets/7cb4389a-245b-4374-927d-da6dbc6e1079" />
 

SwitchB

 <img width="622" height="546" alt="image" src="https://github.com/user-attachments/assets/acc37780-1b64-49ec-8df7-beb7ad853853" />


SwitchC

 <img width="719" height="649" alt="image" src="https://github.com/user-attachments/assets/904a6d12-2038-4f73-85f6-19b4c106644d" />


I then pinged the host from network to network from different nodes to test connectivity using the ping command 

 <img width="702" height="1144" alt="image" src="https://github.com/user-attachments/assets/70377b14-086d-4dfc-9575-805e8312c0a9" />


<img width="808" height="976" alt="image" src="https://github.com/user-attachments/assets/31d7f3d6-9938-427c-bff3-53692776a1e2" />

 
