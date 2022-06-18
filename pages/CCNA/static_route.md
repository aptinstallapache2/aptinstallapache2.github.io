---
title: STATIC ROUTE
summary: "Cấu hình định tuyến tĩnh cho Router"
sidebar: mydoc_sidebar
permalink: static_route.html
folder: CCNA
---

![image](https://user-images.githubusercontent.com/56266496/170835633-cd538524-e5af-4519-82bc-f0596de33a86.png)

## I. Static route

| Syntax |
|:---|
| R(config)#**ip route** < ip-network > < subnet-mask > < nexthop/interface > < metric > |

**Bước 1:** cấu hình các interfaces

* **R1**

```
R1>enable
R1#configure terminal
R1(config)#interface GigabitEthernet0/0
R1(config-if)#ip address 172.16.0.1 255.255.0.0
R1(config-if)#no shutdown
R1(config-if)#exit
R1(config)#interface GigabitEthernet0/1
R1(config-if)#ip address 192.168.1.254 255.255.255.0
R1(config-if)#no shutdown
```

* **R2**

```
R2>enable
R2#configure terminal
R2(config)#interface GigabitEthernet0/0
R2(config-if)#ip address 172.16.0.2 255.255.0.0
R2(config-if)#no shutdown
R2(config-if)#exit
R2(config)#interface GigabitEthernet0/1
R2(config-if)#ip address 223.17.0.1 255.255.0.0
R2(config-if)#no shutdown
R2(config-if)#exit
R2(config)#interface GigabitEthernet0/2
R2(config-if)#ip address 192.168.2.254 255.255.255.0
R2(config-if)#no shutdown
```

* **R3**

```
R3>enable
R3#configure terminal
R3(config)#interface GigabitEthernet0/0
R3(config-if)#ip address 223.17.0.2 255.255.0.0
R3(config-if)#no shutdown
R3(config-if)#exit
R3(config)#interface GigabitEthernet0/1
R3(config-if)#ip address 192.168.3.254 255.255.255.0
R3(config-if)#no shutdown
```

**Bước 2:** Cấu hình static route

* **R1**

```
R1(config)#ip route 192.168.2.0 255.255.255.0 172.16.0.2
R1(config)#ip route 192.168.3.0 255.255.255.0 172.16.0.2
```

* **R2**

```
R2(config)#ip route 192.168.1.0 255.255.255.0 172.16.0.1
R2(config)#ip route 192.168.3.0 255.255.255.0 223.17.0.2
```

* **R3**

```
R3(config)#ip route 192.168.1.0 255.255.255.0 223.17.0.1
R3(config)#ip route 192.168.2.0 255.255.255.0 223.17.0.1
```


## II. Summary và static route

![image](https://user-images.githubusercontent.com/56266496/170828131-cf14ba08-a8a9-42eb-877d-ad2f50b35b13.png)

* **R1**

```
R1(config)#ip route 192.168.1.0 255.255.255.192 102.16.0.2
R1(config)#ip route 192.168.1.192 255.255.255.192 102.16.0.2
R1(config)#ip route 192.168.1.128 255.255.255.192 102.16.0.2
R1(config)#ip route 172.17.0.0 255.255.0.0 102.16.0.2
```

* **R2**

```
R2(config)#ip route 192.168.1.64 255.255.255.192 102.16.0.1
R2(config)#ip route 192.168.1.128 255.255.255.192 172.17.0.2
```

* **R3**

```
R3(config)#ip route 192.168.1.0 255.255.255.192 172.17.0.1
R3(config)#ip route 192.168.1.64 255.255.255.192 172.17.0.1
R3(config)#ip route 192.168.1.192 255.255.255.192 172.17.0.1
R3(config)#ip route 102.16.0.0 255.255.0.0 172.17.0.1
```

## III. Metric và static route

![image](https://user-images.githubusercontent.com/56266496/171597082-2f97d967-4c20-4fd0-a119-01702d2a8cf9.png)

* **R1**

```
R1(config)#ip route 192.168.2.0 255.255.255.0 10.0.0.2
R1(config)#ip route 192.168.2.0 255.255.255.0 20.0.0.2 10
```

* **R2**

```
R2(config)#ip route 192.168.1.0 255.255.255.0 10.0.0.1
R2(config)#ip route 192.168.1.0 255.255.255.0 20.0.0.1 10
```

## IV. Default route

![image](https://user-images.githubusercontent.com/56266496/171996498-7eda5941-4908-4a5c-a7c6-0b796ff1883f.png)

* **R2**

```
R2(config)#ip route 192.168.1.0 255.255.255.0 172.22.0.1
```

* **R1**

```
R1(config)#ip route 0.0.0.0 0.0.0.0 172.22.0.2
```
