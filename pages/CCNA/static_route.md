---
title: STATIC ROUTE
summary: "Cấu hình định tuyến tĩnh cho Router"
sidebar: mydoc_sidebar
permalink: static_route.html
folder: CCNA
---

## I. Static route

## II. Summary và static route

![image](https://user-images.githubusercontent.com/56266496/170828131-cf14ba08-a8a9-42eb-877d-ad2f50b35b13.png)

**R1**

```
R1(config)#ip route 192.168.1.0 255.255.255.192 102.16.0.2
R1(config)#ip route 192.168.1.192 255.255.255.192 102.16.0.2
R1(config)#ip route 192.168.1.128 255.255.255.192 102.16.0.2
R1(config)#ip route 172.17.0.0 255.255.0.0 102.16.0.2
```

**R2**

```
R2(config)#ip route 192.168.1.64 255.255.255.192 102.16.0.1
R2(config)#ip route 192.168.1.128 255.255.255.192 172.17.0.2
```

**R3**

```
R3(config)#ip route 192.168.1.0 255.255.255.192 172.17.0.1
R3(config)#ip route 192.168.1.64 255.255.255.192 172.17.0.1
R3(config)#ip route 192.168.1.192 255.255.255.192 172.17.0.1
R3(config)#ip route 102.16.0.0 255.255.0.0 172.17.0.1
```
