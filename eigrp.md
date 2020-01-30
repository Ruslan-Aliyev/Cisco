# EIGRP

![](https://raw.githubusercontent.com/Ruslan-Aliyev/Cisco/master/Illustrations/eigrp.PNG)

## The following code configures Router 1

The equivalent shall be done for Routers 2 and 3

```				
Router>enable
Router#conf t

Router(config)#int fa0/0
Router(config-if)#ip address 192.168.5.126 255.255.255.128
Router(config-if)#no shutdown

Router(config-if)#int s0/0/0
Router(config-if)#ip address 192.168.5.225 255.255.255.252
Router(config-if)#no shutdown

Router(config-if)#int s0/0/1
Router(config-if)#ip address 192.168.5.233 255.255.255.252
Router(config-if)#clock rate 64000
Router(config-if)#no shutdown
Router(config-if)#exit

Router(config)#router eigrp 1
Router(config-router)#network 192.168.5.0 0.0.0.127
Router(config-router)#network 192.168.5.224 0.0.0.3
Router(config-router)#network 192.168.5.232 0.0.0.3
Router(config-router)#end

Router#show ip route
Codes: C - connected, S - static, I - IGRP, R - RIP, M - mobile, B - BGP
       D - EIGRP, EX - EIGRP external, O - OSPF, IA - OSPF inter area
       N1 - OSPF NSSA external type 1, N2 - OSPF NSSA external type 2
       E1 - OSPF external type 1, E2 - OSPF external type 2, E - EGP
       i - IS-IS, L1 - IS-IS level-1, L2 - IS-IS level-2, ia - IS-IS inter area
       * - candidate default, U - per-user static route, o - ODR
       P - periodic downloaded static route

Gateway of last resort is not set

     192.168.5.0/24 is variably subnetted, 6 subnets, 4 masks
C       192.168.5.0/25 is directly connected, FastEthernet0/0
D       192.168.5.128/26 [90/2172416] via 192.168.5.226, 00:02:52, Serial0/0/0
D       192.168.5.192/27 [90/2172416] via 192.168.5.234, 00:01:14, Serial0/0/1
C       192.168.5.224/30 is directly connected, Serial0/0/0
D       192.168.5.228/30 [90/2681856] via 192.168.5.226, 00:02:38, Serial0/0/0
                         [90/2681856] via 192.168.5.234, 00:01:14, Serial0/0/1
C       192.168.5.232/30 is directly connected, Serial0/0/1		
```
