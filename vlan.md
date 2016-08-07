# VLAN

![](https://raw.githubusercontent.com/atabegruslan/Cisco/master/Illustrations/vlan.PNG)

## The configurations follows:

## FOR THE ROUTER

```
Router>enable
Router#config term
Router(config)#int fa0/1
Router(config-if)#no shutdown

Router(config-if)#int fa0/1.1
Router(config-subif)#encap dot1q 1
Router(config-subif)#ip address 172.17.1.1 255.255.255.0

Router(config-subif)#int fa0/1.10
Router(config-subif)#encap dot1q 10
Router(config-subif)#ip address 172.17.10.1 255.255.255.0

Router(config-subif)#int fa0/1.20
Router(config-subif)#encap dot1q 20
Router(config-subif)#ip address 172.17.20.1 255.255.255.0

Router(config-subif)#int fa0/1.30
Router(config-subif)#encap dot1q 30
Router(config-subif)#ip address 172.17.30.1 255.255.255.0

Router(config-subif)#int fa0/1.99
Router(config-subif)#encap dot1q 99 nat
Router(config-subif)#ip address 172.17.99.1 255.255.255.0
```

## FOR SWITCH 1

```
Switch>enable
Switch#config term
Switch(config)#hostname s1
s1(config)#no ip domain-lookup

s1(config)#ip default-gate 172.17.99.1

s1(config)#vtp mode server
s1(config)#vtp domain dom1
s1(config)#vtp password th1s

s1(config)#int range fa0/1-5
s1(config-if-range)#switchport mode trunk
s1(config-if-range)#switchport trunk native vlan 99
s1(config-if-range)#no shutdown
s1(config-if-range)#exit

s1(config)#vlan 99
s1(config-vlan)#name manage
s1(config-vlan)#exit

s1(config)#vlan 10
s1(config-vlan)#name faculty1
s1(config-vlan)#exit

s1(config)#vlan 20
s1(config-vlan)#name faculty2
s1(config-vlan)#exit

s1(config)#vlan 30
s1(config-vlan)#name faculty3
s1(config-vlan)#exit

s1(config)#int vlan 99
s1(config-if)#ip add 172.17.99.11 255.255.255.0
```

## FOR SWITCH 2

```
Switch>enable
Switch#config term
Switch(config)#int fa 0/6
Switch(config-if)#switchport mode access
Switch(config-if)#no shutdown

Switch(config-if)#int fa 0/11
Switch(config-if)#switchport mode access
Switch(config-if)#no shutdown

Switch(config-if)#int fa 0/18
Switch(config-if)#switchport mode access
Switch(config-if)#no shutdown
Switch(config-if)#exit

Switch(config)#vtp mode client
Switch(config)#vtp domain dom1
Switch(config)#vtp password th1s

Switch(config)#int range fa0/1-5
Switch(config-if-range)#switchport mode trunk
Switch(config-if-range)#switchport trunk native vlan 99
Switch(config-if-range)#no shutdown
Switch(config-if-range)#exit

Switch(config)#int vlan 99
Switch(config-if)#ip address 172.17.99.13 255.255.255.0
Switch(config-if)#exit

Switch(config)#int range fa0/6-10
Switch(config-if-range)#switchport access vlan 30

Switch(config-if-range)#int range fa0/11-17
Switch(config-if-range)#switchport access vlan 10

Switch(config-if-range)#int range fa0/18-24
Switch(config-if-range)#switchport access vlan 20
```

## FOR SWITCH 3

```
Switch>enable
Switch#config term

Switch(config)#vtp mode client
Switch(config)#vtp domain dom1
Switch(config)#vtp password th1s

Switch(config)#int range fa0/1-5
Switch(config-if-range)#switchport mode trunk
Switch(config-if-range)#switchport trunk native vlan 99
Switch(config-if-range)#no shutdown
Switch(config-if-range)#exit

Switch(config)#int vlan 99
Switch(config-if)#ip add 172.17.99.12 255.255.255.0		
```
