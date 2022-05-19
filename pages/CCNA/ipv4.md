---
title: IP VERSION 4
summary: "Địa chỉ IPv4"
sidebar: mydoc_sidebar
permalink: ipv4.html
folder: CCNA
---

Toàn bộ địa chỉ IP được chia thành 5 nhóm gọi là Class IP. 5 nhóm này phân biệt dựa vào giá trị nhóm octet đầu tiên như sau:

|  | Class | First octet | Default Subnet Mask | Function |
| --- | --- | --- | --- | --- |
| 0------- | A | 1 - 126 | 255.0.0.0 | Unicast (IP riêng) / Broadcast (IP quảng bá) |
| 10------ | B | 128 - 191 | 255.255.0.0 | Unicast (IP riêng) / Broadcast (IP quảng bá) |
| 110----- | C | 192 - 223 | 255.255.255.0 | Unicast (IP riêng) / Broadcast (IP quảng bá) |
| 1110---- | D | 224 - 239 | --- | Multicast (IP nhóm) |
| 1111---- | E | 240 - 255 | --- | Experimental |

Bảng phân hoạch IP:

| Số bit mượn (n) | Số subnet (2^n) | Bước nhảy 2^(8-n) | Subnet mask |
| --- | --- | --- | --- |
| 1 | 2 | 128 | 128 |
| 2 | 4 | 64 | 192 |
| 3 | 8 | 32 | 224 |
| 4 | 16 | 16 | 240 |
| 5 | 32 | 8 | 248 |
| 6 | 64 | 4 | 252 |
| 7 | 128 | 2 | 254 |
| 8 | 256 | 1 | 255 |
