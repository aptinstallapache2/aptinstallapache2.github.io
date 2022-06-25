---
title: OSPF ROUTE (SINGLE AREA)
summary: "Cấu hình định tuyến động sử dụng giao thức OSPF cho Router"
sidebar: mydoc_sidebar
permalink: ospf_route_single_area.html
folder: CCNA
---

Giao thức điển hình của giải thuật Link State hay còn được gọi là Shortest Path First (SPF). Mỗi router khi chạy giao thức sẽ gửi các trạng thái đường link của nó cho tất cả các router trong vùng (area). Sau một thời gian trao đổi, các router sẽ đồng nhất được bảng cơ sở dữ liệu trạng thái đường link (Link State Database - LSDB) với nhau, mỗi router đều có được "bản đồ mạng" của cả vùng. Từ đó mỗi router sẽ chạy giải thuật Dijkstra tính toán ra một cây đường đi ngắn nhất (Shortest Path Tree) và dựa vào cây này để xây dựng nên bảng định tuyến.

Quy trình hoạt động cơ bản:

* Gửi gói tin hello quảng bá về bản thân với chu kì 10s với mạng quảng bá đa truy cập (broadcast multi-access) và 30s cho dead.
* Bên cạnh đó quảng bá và thu các gói tin về trạng thái đường đi đến các router láng giềng - gói Link State Advertisement (LSA).
* Dùng thuật toán Dijkstra xây dựng sơ đồ Shortest Path Tree (SPT) - bản đồ thống nhất về các router trong vùng và khoảng cách, băng thông giữa chúng theo router tính toán.
* Tính toán đường đi tối ưu.
* Bản đồ được lưu vào Link State Database (LSD).

![image](https://user-images.githubusercontent.com/56266496/170835633-cd538524-e5af-4519-82bc-f0596de33a86.png)

## Cách 1

| Syntax |
|:---|
| R(config)#router ospf < process-id > <br/> R(config-router)#exit <br/> R(config)#int < direct-interface > <br/> R(config-if)#ip ospf < process-id  > area < area-id > |

* **R1**

```
R1(config)#router ospf 1
R1(config-router)#exit

R1(config)#int Gi0/0
R1(config-if)#ip ospf 1 area 0

R1(config)#int Gi0/1
R1(config-if)#ip ospf 1 area 0
```

* **R2**

```
R2(config)#router ospf 1
R2(config-router)#exit

R2(config)#int Gi0/0
R2(config-if)#ip ospf 1 area 0

R2(config)#int Gi0/1
R2(config-if)#ip ospf 1 area 0

R2(config)#int Gi0/2
R2(config-if)#ip ospf 1 area 0
```

* **R3**

```
R3(config)#router ospf 1
R3(config-router)#exit

R3(config)#int Gi0/0
R3(config-if)#ip ospf 1 area 0

R3(config)#int Gi0/1
R3(config-if)#ip ospf 1 area 0
```

## Cách 2 (recommend)

| Syntax |
|:---|
| R(config)#router ospf < process-id > <br/> R(config-router)#network < direct-hop > 0.0.0.0 area < area-id > |

* **R1**

```
R1(config)#router ospf 1
R1(config-router)#network 172.16.0.1 0.0.0.0 area 0
R1(config-router)#network 192.168.1.254 0.0.0.0 area 0
```

* **R2**

```
R2(config)#router ospf 1
R2(config-router)#network 172.16.0.2 0.0.0.0 area 0
R2(config-router)#network 223.17.0.1 0.0.0.0 area 0
R2(config-router)#network 192.168.2.254 0.0.0.0 area 0
```

* **R3**

```
R3(config)#router ospf 1
R3(config-router)#network 223.17.0.1 0.0.0.0 area 0
R3(config-router)#network 192.168.3.254 0.0.0.0 area 0
```

## Cách 3

| Syntax |
|:---|
| R(config)#router ospf < process-id > <br/> R(config-router)#network < direct-net > < wildcard-mask > area < area-id > |

* **R1**

```
R1(config)#router ospf 1
R1(config-router)#network 172.16.0.0 0.0.255.255 area 0
R1(config-router)#network 192.168.1.0 0.0.0.255 area 0
```

* **R2**

```
R2(config)#router ospf 1
R2(config-router)#network 172.16.0.0 0.0.255.255 area 0
R2(config-router)#network 223.17.0.0 0.0.255.255 area 0
R2(config-router)#network 192.168.2.0 0.0.0.255 area 0
```

* **R3**

```
R3(config)#router ospf 1
R3(config-router)#network 223.17.0.0 0.0.255.255 area 0
R3(config-router)#network 192.168.3.0 0.0.0.255 area 0
```

## Các lệnh debug

```
R# sh ip int bri
R# sh ip ospf
R# sh ip ospf int
R# sh ip ospf nei
```

