![image](https://user-images.githubusercontent.com/56266496/176694085-63b64e91-7977-4faa-828b-0da59352603c.png)

## Chia vlan

```
SW1(config)#int g0/1
SW1(config-if)#switchport mode trunk
```

```
SW1(config)#vlan 101
SW1(config-vlan)#name Hanhchanh
SW1(config-vlan)#vlan 102
SW1(config-vlan)#name Kinhdoanh
SW1(config-vlan)#vlan 103
SW1(config-vlan)#name Ketoan

SW1(config)#vtp mode server
SW1(config)#vtp domain ABC
SW1(config)#vtp pass 123
```

```
SW2(config)#vtp mode client
SW2(config)#vtp domain ABC
SW2(config)#vtp pass 123
```

```
SW1(config)#int range f0/1-2
SW1(config-if-range)#switchport mode access 
SW1(config-if-range)#switchport access vlan 101
```

## Inter Vlan

### Cach 1: Sub interface

```
R(config)#int g0/0
R(config-if)#no shut
R(config-if)#ip address 192.168.1.254 255.255.255.0

R(config-if)#int g0/0.1
R(config-subif)#encapsulation dot1Q 101
R(config-subif)#ip address 192.168.101.254 255.255.255.0
R(config-subif)#int g0/0.2
R(config-subif)#encapsulation dot1Q 102
R(config-subif)#ip address 192.168.102.254 255.255.255.0
R(config-subif)#int g0/0.3
R(config-subif)#encapsulation dot1Q 103
R(config-subif)#ip address 192.168.103.254 255.255.255.0
```

### Cach 2:

```
conf t
ip routing
int vlan 1
no shut
ip add 192.168.1.254 255.255.255.0
int vlan 101
ip add 192.168.101.254 255.255.255.0
int vlan 102
ip add 192.168.102.254 255.255.255.0
int vlan 103
ip add 192.168.103.254 255.255.255.0
```