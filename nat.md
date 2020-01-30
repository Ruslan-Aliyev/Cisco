# NAT

![](https://raw.githubusercontent.com/Ruslan-Aliyev/Cisco/master/Illustrations/nat.PNG)

## Configuration for the router follows: 

```
Router>enable
Router#conf t

Router(config)#int fa0/0
Router(config-if)#ip address 192.168.0.254 255.255.255.0
Router(config-if)#no shutdown

Router(config-if)#int fa0/1
Router(config-if)#ip address 30.0.0.1 255.0.0.0
Router(config-if)#no shutdown
Router(config-if)#exit

Router(config)#ip route 0.0.0.0 0.0.0.0 fa0/1
Router(config)#access-list 1 permit 192.168.0.0 0.0.0.255
Router(config)#ip nat pool poolname 50.0.0.1 50.0.0.5 netmask 255.0.0.0
Router(config)#ip nat inside source list 1 pool poolname

Router(config)#int fa0/0
Router(config-if)#ip nat inside
Router(config-if)#int fa0/1
Router(config-if)#ip nat outside
Router(config-if)#end


Router#debug ip nat
IP NAT debugging is on
Router#
NAT: s=192.168.0.1->50.0.0.1, d=30.0.0.2 [7]

NAT*: s=30.0.0.2, d=50.0.0.1->192.168.0.1 [4]

NAT*: s=192.168.0.1->50.0.0.1, d=30.0.0.2 [8]

NAT*: s=192.168.0.1->50.0.0.1, d=30.0.0.2 [9]

NAT*: s=30.0.0.2, d=50.0.0.1->192.168.0.1 [5]

NAT*: s=192.168.0.1->50.0.0.1, d=30.0.0.2 [10]

NAT*: s=30.0.0.2, d=50.0.0.1->192.168.0.1 [6]

NAT*: s=192.168.0.1->50.0.0.1, d=30.0.0.2 [11]				
```
