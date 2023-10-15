---
title: PPPoE
summary: "Các lệnh cấu hình PPPoE"
sidebar: mydoc_sidebar
permalink: pppoe.html
folder: CCNA
---

	Modem1 (e0/0)------------(e0/1) SW (e0/0)------------(e0/1) BRAS
	Modem2 (e0/0)------------(e0/2) -┘

* __BRAS__

```
en
conf t
hostname BRAS
!
username ftth_u1 password 123
!
bba-group pppoe NHATNGHE
 virtual-template 1
!
interface Virtual-Template1
 mtu 1492
 ip unnumbered Ethernet0/1
 peer default ip address pool NN_DHCP
 ppp authentication chap callin
!
interface Ethernet0/1
 no shutdown
 no ip address
 ip address 210.245.0.1 255.255.255.0
 pppoe enable group NHATNGHE
!
ip local pool NN_DHCP 210.245.0.2 210.245.0.254
!
end
write

```

* __Modem1__

```
en
conf t
hostname Modem1
!
interface Ethernet0/0
 no shutdown
 no ip address
 pppoe enable
 pppoe-client dial-pool-number 1
!
interface Dialer0
 mtu 1492
 ip address negotiated
 encapsulation ppp
 dialer pool 1
 ppp authentication chap callin
 ppp pap sent-username ftth_u1 password 123
!
end
write

```

```
en
conf t
hostname Modem1
!
interface Ethernet0/0
 no shutdown
 no ip address
 pppoe enable
 pppoe-client dial-pool-number 1
!
interface Dialer0
 mtu 1492
 ip address negotiated
 encapsulation ppp
 dialer pool 1
 ppp chap hostname ftth_u1
 ppp chap password 123
!
end
write

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

	LAN ----(e0/1) Modem1 (e0/0 - Dialer1: pppoe)  ------- Internet

vd: Modem1 cấu hình NAT

	conf t
	access-list 1 permit any
	(ip nat inside source list 1 int e0/0 overload)
	ip nat inside source list 1 int dialer 1 overload
	int DIALER 1
	ip nat outside
	int e0/1
	ip nat inside
	
VPN theo sơ đồ trong bài học, phải thay cổng f0/1 bằng Dialer 1
	int f0/1 ---> int dialer 1
	crypto map MAP1
```
