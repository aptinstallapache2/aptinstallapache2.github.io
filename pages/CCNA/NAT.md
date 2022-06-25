---
title: NAT - Network Address Translation
summary: "Biên dịch địa chỉ mạng"
sidebar: mydoc_sidebar
permalink: nat.html
folder: CCNA
---

**Phân loại**
* NAT : IP
* PAT (Port Address Translation) : IP+Port

**Các kiểu cấu hình**
* static: one to one
* dynamic: one to many 

Trước khi cấu hình NAT cần cấu hình default route cho router

![image](https://user-images.githubusercontent.com/56266496/175782690-fe89a6aa-67d1-4ebc-ba26-a4b95855dea6.png)

## NAT static

* __R1__

Cấu hình nat

```
R1(config)#ip nat inside source static 192.168.1.1 10.0.0.1
R1(config)#ip nat inside source static 192.168.1.2 20.0.0.1
```

Cấu hình interface

```
R1(config)#int g0/0
R1(config-if)#ip nat outside
R1(config-if)#int g0/1
R1(config-if)#ip nat inside
```

## NAT dynamic

* __R1__

```
R1(config)#access-list 1 permit any
R1(config)#ip nat pool 1 10.0.0.1 10.0.0.2 netmask 255.0.0.0
R1(config)#ip nat inside source list 1 pool 1
```

## PAT dynamic

Cách 1

```
R1(config)#access-list 1 permit any
R1(config)#ip nat pool 1 10.0.0.1 10.0.0.2 netmask 255.0.0.0
R1(config)#ip nat inside source list 1 pool 1 overload
```

Cách 2

```
R1(config)#access-list 1 permit any
R1(config)#ip nat inside source list 1 int g0/1 overload
```

## PAT static (NAT port forwarding)

```
R1(config)#ip nat inside source static tcp 192.168.1.2 80 20.0.0.1 5000
```
