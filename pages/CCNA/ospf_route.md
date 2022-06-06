---
title: OSPF ROUTE
summary: "Cấu hình định tuyến động sử dụng giao thức OSPF cho Router"
sidebar: mydoc_sidebar
permalink: ospf_route.html
folder: CCNA
---

![image](https://user-images.githubusercontent.com/56266496/170835633-cd538524-e5af-4519-82bc-f0596de33a86.png)

## Cách 1

```
R(config)#router ospf <PROCESS-ID>
R(config-router)#exit
R(config)#int <INTERFACE-ĐẤU-NỐI-TRỰC-TIẾP>
R(config-if)#ip ospf <PROCESS-ID> area <AREA-ID>
```

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

```
R(config)#router ospf <PROCESS-ID>
R(config-router)#network <IP-INTERFACE-ĐẤU-NỐI-TRỰC-TIẾP> 0.0.0.0 area <AREA-ID>
```

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

```
R(config)#router ospf <PROCESS-ID>
R(config-router)#network <IP-NETWORK-ĐẤU-NỐI-TRỰC-TIẾP> <WILDCARD-MASK> area <AREA-ID>
```

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

* **Các lệnh debug**

```
R# sh ip int bri
R# sh ip ospf
R# sh ip ospf int
R# sh ip ospf nei
```

