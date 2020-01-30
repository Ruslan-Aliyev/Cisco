# Frame Relay

![](https://raw.githubusercontent.com/Ruslan-Aliyev/Cisco/master/Illustrations/fr_subif_1.PNG)

![](https://raw.githubusercontent.com/Ruslan-Aliyev/Cisco/master/Illustrations/fr_subif_2.PNG)

## Configuration for Router 2 follows: 

The equivalent shall be done for Routers 1 and 3.

```
Router>enable
Router#conf t

Router(config-if)#int fa0/0
Router(config-if)#ip address 172.16.0.1 255.255.255.0
Router(config-if)#no shutdown

Router(config)#int s0/0/0
Router(config-if)#ip address 10.0.0.2 255.0.0.0
Router(config-if)#no shutdown
Router(config-if)#exit

Router(config)#router rip
Router(config-router)#network 172.16.0.0
Router(config-router)#network 10.0.0.0
Router(config-router)#exit

Router(config)#hostname R2

R2(config)#int s0/0/0
R2(config-if)#no ip address 10.0.0.2 255.0.0.0
R2(config-if)#encap frame-relay

R2(config-if)#int s0/0/0.201 point-to-point
R2(config-subif)#ip address 10.0.0.1 255.255.255.0
R2(config-subif)#bandwidth 64
R2(config-subif)#frame-relay interface-dlci 201

R2(config-subif)#int s0/0/0.203 point-to-point
R2(config-subif)#ip address 10.0.1.3 255.255.255.0
R2(config-subif)#bandwidth 64
R2(config-subif)#frame-relay interface-dlci 203		
```
