# OSPF

![](https://raw.githubusercontent.com/atabegruslan/Cisco/master/Illustrations/ospf.PNG)

## Configuration for the router follows: 

```
Continue with configuration dialog? [yes/no]: n

Press RETURN to get started!

Router>enable
Router#config t
Router(config)#hostname r1
r1(config)#no ip domain-lookup

r1(config)#int fa 0/0
r1(config-if)#ip add 192.168.1.30 255.255.255.224
r1(config-if)#no shut
r1(config-if)#exit

r1(config)#int s0/0/0
r1(config-if)#ip add 192.168.1.162 255.255.255.224
r1(config-if)#clock rate 64000
r1(config-if)#no shut
r1(config-if)#exit

r1(config)#int s0/0/1
r1(config-if)#ip add 192.168.1.97 255.255.255.224
r1(config-if)#no shut
r1(config-if)#exit

r1(config)#router ospf 1
r1(config-router)#netw 192.168.1.160 0.0.0.31 area 0
r1(config-router)#netw 192.168.1.98 0.0.0.31 area 0
r1(config-router)#netw 192.168.1.0 0.0.0.31 area 0

r1(config-router)#passive-int fa0/0

r1(config-router)#end


r1#show ip route
Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
       * - candidate default, U - per-user static route, o - ODR
       P - periodic downloaded static route
Gateway of last resort is not set
     192.168.1.0/27 is subnetted, 6 subnets
C       192.168.1.0 is directly connected, FastEthernet0/0
O       192.168.1.32 [110/65] via 192.168.1.161, 00:16:54, Serial0/0/0
O       192.168.1.64 [110/65] via 192.168.1.98, 00:15:58, Serial0/0/1
C       192.168.1.96 is directly connected, Serial0/0/1
O       192.168.1.128 [110/128] via 192.168.1.161, 00:24:14, Serial0/0/0
                      [110/128] via 192.168.1.98, 00:24:14, Serial0/0/1
C       192.168.1.160 is directly connected, Serial0/0/0

r1#show ip ospf neighbor
Neighbor ID     Pri   State           Dead Time   Address         Interface
192.168.1.161     0   FULL/  -        00:00:31    192.168.1.161   Serial0/0/0
192.168.1.130     0   FULL/  -        00:00:35    192.168.1.98    Serial0/0/1
r1#					
```
