---
title: ETHERCHANNEL
summary: "Ghép nối các đường liên kết dùng cho chia tải"
sidebar: mydoc_sidebar
permalink: etherchannel.html
folder: CCNA
---

__Mục đích__: ghép nối các đường liên kết vật lý thành 1 liên kết logic giúp tăng băng thông cho kết nối 2 thiết bị.

__Cấu hình__:

```
SW1(config)#int range g0/1-2
SW1(config-if-range)#channel-group 1 mode active 

SW2(config)#int range g0/1-2
SW2(config-if-range)#channel-group 1 mode passive 
```

![image](./img/pagp-lacp.png)

Bảng chia tải (Load balancing) cho Etherchannel:

| Configuration Keyword | Math Uses...                    | Layer |
|:----------------------|:--------------------------------|:------|
| src-mac               | Source MAC address              | 2     |
| dst-mac               | Destination MAC address         | 2     |
| src-dst-mac           | Both source and destination MAC | 2     |
| src-ip                | Source IP address               | 2     |
| src-ip                | Destination IP address          | 2     |
| src-ip                | Both source and destination IP  | 2     |

```
SW1(config)#port-channel load-balance src-dst-mac

SW2(config)#port-channel load-balance src-dst-mac
```
