---
title: PPPoE
summary: "Các lệnh cấu hình PPPoE"
sidebar: mydoc_sidebar
permalink: pppoe.html
folder: CCNA
---

	R1 ------------(G0/0) SW1 (G0/0)------------ISP
	R2 ------------(G0/0) -┘

* __ISP__

```
en
conf t
hostname ISP
username ftth_u1 password 123
bba-group pppoe NHATNGHE
virtual-template 1
exit
interface Virtual-Template1
peer default ip address pool NN_DHCP
ppp authentication chap callin
ip unnumbered G0/1
ppp authentication chap
interface G0/0
no ip address
no shut
pppoe enable group NHATNGHE

interface G0/1
ip address 210.245.0.1 255.255.255.0
ip local pool NN_DHCP 210.245.0.2 210.245.0.254
```

* __R1__

```
en
conf t
hostname R1

interface G0/0
 no shut
 no ip address
 pppoe enable
 pppoe-client dial-pool-number 1
 
interface Dialer1
 dialer pool 1
 ip address negotiated
 mtu 1492
 encapsulation ppp
 ppp chap hostname ftth_u1
 ppp chap password 123
```

* __Test__

```
show pppoe session
show ip int brief
ping 210.245.0.1
```

```
GHI CHÚ:

Nếu có PPPoE thì phải sửa cấu hình: NAT, VPN thành cổng Dialer thay cho cổng Vật lý

	LAN ----(G0/1) R1 (G0/0 - Dialer1: pppoe)  ------- Internet

vd: R1 cấu hình NAT

	conf t
	access-list 1 permit any
	(ip nat inside source list 1 int g0/0 overload)
	ip nat inside source list 1 int dialer 1 overload
	int DIALER 1
	ip nat outside
	int g0/1
	ip nat inside
	
VPN theo sơ đồ trong bài học, phải thay cổng f0/1 bằng Dialer 1
	int f0/1 ---> int dialer 1
	crypto map MAP1
```
