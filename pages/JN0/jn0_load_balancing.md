---
title: Load Balancing
summary: "Load Balancing"
sidebar: mydoc_sidebar
permalink: jn0_load_balancing.html
folder: JN0
---

## Notes

Mặc định, Junos OS quyết định luồng lưu lượng dựa vào 4 keys sau:

|                          |                     |
|:-------------------------|:--------------------|
| Incoming Interface Index | Destination Address |
| Source Address           | Protocol            |

Chính sách cân bằng tải được tạo trong Junos OS luôn chứa cùng cú pháp cấu hình "`load-balance per-packet`". Tuy nhiên, hành vi cân bằng tải thực tế phụ thuộc vào nền tảng của thiết bị.

Internet Processor I -> per-packet (Có trên các thiết bị Junos cũ)

Internet Processor II -> per-flow (Có trên các thiết bị Junos hiện đại)

`per-flow` > `per-packet`. Per-packet giúp cân bằng tải tốt hơn nhưng gây sắp xếp lại gói tin, giảm hiệu suất mạng. Per-flow cân bằng tải theo luồng, không cần sắp xếp lại gói tin, độ trễ thấp.

## Chuẩn bị

![](img/7.png)

```
# vMX1

set interfaces ge-0/0/0 unit 0 family inet address 10.0.0.1/29
set interfaces ge-0/0/1 unit 0 family inet address 10.0.1.1/29
set interfaces lo0 unit 0 family inet address 1.1.1.1/32

set protocols ospf area 0.0.0.0 interface lo0.0
set protocols ospf area 0.0.0.0 interface ge-0/0/0.0
set protocols ospf area 0.0.0.0 interface ge-0/0/1.0

# vMX2

set interfaces ge-0/0/0 unit 0 family inet address 10.0.0.2/29
set interfaces ge-0/0/1 unit 0 family inet address 10.0.1.2/29
set interfaces lo0 unit 0 family inet address 2.2.2.2/32

set protocols ospf area 0.0.0.0 interface lo0.0
set protocols ospf area 0.0.0.0 interface ge-0/0/0.0
set protocols ospf area 0.0.0.0 interface ge-0/0/1.0
```

## Kiểm tra trước khi chưa Load-Balancing

```
root@vMX1> show route 2.2.2.2/32

inet.0: 7 destinations, 7 routes (7 active, 0 holddown, 0 hidden)
+ = Active Route, - = Last Active, * = Both

2.2.2.2/32         *[OSPF/10] 00:02:50, metric 1
                      to 10.0.0.2 via ge-0/0/0.0
                    > to 10.0.1.2 via ge-0/0/1.0

root@vMX1> show route forwarding-table | match 2.2.2.2/32
2.2.2.2/32         user     0 10.0.1.2           ucst      562     3 ge-0/0/1.0
```

## Cấu hình chính sách Load-Balancing

```
# vMX1

set policy-options policy-statement LOAD_BALANCE then load-balance per-packet
set routing-options forwarding-table export LOAD_BALANCE
```

## Kiểm tra sau khi Load-Balancing

```
root@vMX1> show route forwarding-table | find 2.2.2.2/32
2.2.2.2/32         user     0                    ulst  1048574     2
                              10.0.0.2           ucst      561     2 ge-0/0/0.0
                              10.0.1.2           ucst      562     2 ge-0/0/1.0
```