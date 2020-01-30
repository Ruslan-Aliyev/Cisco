# DHCP

![](https://raw.githubusercontent.com/Ruslan-Aliyev/Cisco/master/Illustrations/dhcp.PNG)
						
## Configuration for the router follows: 

```
Router>enable
Router#conf t

Router(config)#int fa0/0
Router(config-if)#ip address 192.168.1.1 255.255.255.0
Router(config-if)#no shutdown
Router(config-if)#exit

Router(config)#ip dhcp pool poolname
Router(dhcp-config)#network 192.168.1.0 255.255.255.0
Router(dhcp-config)#default-router 192.168.1.1
Router(dhcp-config)#exit
Router(config)#ip dhcp excluded-address 192.168.1.2 192.168.1.100	
```
