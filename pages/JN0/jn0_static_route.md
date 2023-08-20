---
title: Static Route
summary: "Static Route"
sidebar: mydoc_sidebar
permalink: jn0_static_route.html
folder: JN0
---

## Static Route

![](img/2.png)

| Syntax |
|:---|
| set routing-options static route `<destination>` next-hop `<next-hop>` |

__Bước 1:__ Cấu hình các interfaces

```
root@vMX1# run show configuration | display set
set system host-name vMX1
set interfaces ge-0/0/0 unit 0 family inet address 172.0.12.1/29
set interfaces lo0 unit 0 family inet address 1.1.1.1/32

root@vMX2# run show configuration | display set
set system host-name vMX2
set interfaces ge-0/0/0 unit 0 family inet address 172.0.23.2/29
set interfaces ge-0/0/1 unit 0 family inet address 172.0.12.2/29
set interfaces lo0 unit 0 family inet address 2.2.2.2/32

root@vMX3# run show configuration | display set
set system host-name vMX3
set interfaces ge-0/0/1 unit 0 family inet address 172.0.23.3/29
set interfaces lo0 unit 0 family inet address 3.3.3.3/32
```

__Bước 2:__ Cấu hình static route

Trích dẫn từ tài liệu JRE:
> "We strongly recommend that you use the `no-readvertise` option on static routes that direct traffic out the management Ethernet interface and through the management network."

```
# vMX1
set routing-options static route 172.0.23.0/29 next-hop 172.0.12.2 no-readvertise
set routing-options static route 2.2.2.2/32 next-hop 172.0.12.2 no-readvertise
set routing-options static route 3.3.3.3/32 next-hop 172.0.12.2 no-readvertise

# vMX2
set routing-options static route 1.1.1.1/32 next-hop 172.0.12.1 no-readvertise
set routing-options static route 3.3.3.3/32 next-hop 172.0.23.3 no-readvertise

# vMX3
set routing-options static route 1.1.1.1/32 next-hop 172.0.23.2 no-readvertise
set routing-options static route 2.2.2.2/32 next-hop 172.0.23.2 no-readvertise
set routing-options static route 172.0.12.0/29 next-hop 172.0.23.2 no-readvertise
```

__Bước 3:__ Kiểm tra

```
root@vMX1> show route

inet.0: 6 destinations, 6 routes (6 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

1.1.1.1/32         *[Direct/0] 00:49:21
                    > via lo0.0
2.2.2.2/32         *[Static/5] 00:30:18
                    > to 172.0.12.2 via ge-0/0/0.0
3.3.3.3/32         *[Static/5] 00:30:18
                    > to 172.0.12.2 via ge-0/0/0.0
172.0.12.0/29      *[Direct/0] 00:41:33
                    > via ge-0/0/0.0
172.0.12.1/32      *[Local/0] 00:41:33
                      Local via ge-0/0/0.0
172.0.23.0/29      *[Static/5] 00:30:38
                    > to 172.0.12.2 via ge-0/0/0.0

root@vMX1# run ping 2.2.2.2 rapid
PING 2.2.2.2 (2.2.2.2): 56 data bytes
!!!!!
--- 2.2.2.2 ping statistics ---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip min/avg/max/stddev = 1.393/1.726/2.039/0.245 ms

[edit]
root@vMX1# run ping 3.3.3.3 rapid
PING 3.3.3.3 (3.3.3.3): 56 data bytes
!!!!!
--- 3.3.3.3 ping statistics ---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip min/avg/max/stddev = 2.079/4.123/10.902/3.400 ms
```

## Static Route Next-Hop Resolution

```
root@vMX1# delete routing-options static route 3.3.3.3/32
root@vMX1# set routing-options static route 3.3.3.3/32 next-hop 172.0.23.3 resolve
root@vMX1# run show route

inet.0: 6 destinations, 6 routes (6 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

1.1.1.1/32         *[Direct/0] 00:57:01
                    > via lo0.0
2.2.2.2/32         *[Static/5] 00:37:58
                    > to 172.0.12.2 via ge-0/0/0.0
3.3.3.3/32         *[Static/5] 00:00:27, metric2 0
                    > to 172.0.12.2 via ge-0/0/0.0
172.0.12.0/29      *[Direct/0] 00:49:13
                    > via ge-0/0/0.0
172.0.12.1/32      *[Local/0] 00:49:13
                      Local via ge-0/0/0.0
172.0.23.0/29      *[Static/5] 00:38:18
                    > to 172.0.12.2 via ge-0/0/0.0

root@vMX1# run ping 3.3.3.3 rapid
PING 3.3.3.3 (3.3.3.3): 56 data bytes
!!!!!
--- 3.3.3.3 ping statistics ---
5 packets transmitted, 5 packets received, 0% packet loss
round-trip min/avg/max/stddev = 2.687/6.506/20.471/6.992 ms
```

## Static Route Qualified Next-Hops

![Alt text](img/3.png)

```
# vMX1
set routing-options static route 2.2.2.2/32 next-hop 172.0.12.2
set routing-options static route 2.2.2.2/32 qualified-next-hop 172.0.12.6 preference 7
```

