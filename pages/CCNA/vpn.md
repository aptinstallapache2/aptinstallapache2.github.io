---
title: VPN
summary: "Mạng riêng ảo"
sidebar: mydoc_sidebar
permalink: vpn.html
folder: CCNA
---

![image](./img/vpn.png)

## GRE Tunnel

* __R1__

```
R1(config)#int tunnel 1
R1(config-if)#ip address 10.0.0.1 255.0.0.0
R1(config-if)#tunnel source g0/0
R1(config-if)#tunnel destination 203.162.2.1
R1(config-if)#tunnel mode gre ip
R1(config-if)#exit
R1(config)#ip route 192.168.2.0 255.255.255.0 10.0.0.2
```

* __R2__

```
R1(config)#int tunnel 1
R1(config-if)#ip address 10.0.0.2 255.0.0.0
R1(config-if)#tunnel source g0/0
R1(config-if)#tunnel destination 203.162.1.1
R1(config-if)#tunnel mode gre ip
R1(config-if)#exit
R1(config)#ip route 192.168.1.0 255.255.255.0 10.0.0.1
```

## IPSEC VPN Site-to-Site

* __R1__

```
R1(config)#crypto isakmp policy 9
R1(config-isakmp)#hash md5
R1(config-isakmp)#group 5
R1(config-isakmp)#authentication pre-share
R1(config-isakmp)#exit
R1(config)#crypto isakmp key 123 address 203.162.2.1
R1(config)#access-list 100 permit ip 192.168.1.0 0.0.0.255 192.168.2.0 0.0.0.255
R1(config)#crypto ipsec transform-set MYSET esp-3des esp-md5-hmac
R1(config)#crypto map MYMAP 10 ipsec-isakmp
R1(config-crypto-map)#set peer 203.162.2.1
R1(config-crypto-map)#set transform-set MYSET
R1(config-crypto-map)#match address 100
R1(config-crypto-map)#exit
R1(config)#int g0/0
R1(config-if)#crypto map MYMAP
```

* __R2__

```
R2(config)#crypto isakmp policy 9
R2(config-isakmp)#hash md5
R2(config-isakmp)#group 5
R2(config-isakmp)#authentication pre-share
R2(config-isakmp)#exit
R2(config)#crypto isakmp key 123 address 203.162.1.1
R2(config)#access-list 100 permit ip 192.168.2.0 0.0.0.255 192.168.1.0 0.0.0.255
R2(config)#crypto ipsec transform-set MYSET esp-3des esp-md5-hmac
R2(config)#crypto map MYMAP 10 ipsec-isakmp
R2(config-crypto-map)#set peer 203.162.1.1
R2(config-crypto-map)#set transform-set MYSET
R2(config-crypto-map)#match address 100
R2(config-crypto-map)#exit
R2(config)#int g0/0
R2(config-if)#crypto map MYMAP
```
