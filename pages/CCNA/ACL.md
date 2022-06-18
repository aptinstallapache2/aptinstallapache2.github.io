---
title: ACCESS CONTROL LIST
summary: "Danh sách điều khiển truy cập"
sidebar: mydoc_sidebar
permalink: acl.html
folder: CCNA
---

**Chức năng**
* Quản lý gói qua cổng : áp vào interface
* Quản lý telnet : áp vào vty
* Quản lý dịch vụ : áp vào dịch vụ tương ứng

**Phân loại**
* Standard (id 1-99)
* Extended (id 100-199)

*Lưu ý: ALC là một danh sách các phát biểu, nếu gói tin không thuộc phát biểu nào sẽ bị deny.*

## I. Standard access list

| Syntax |
|:---|
| access-list < acl-id (1-99) > < permit/deny > < source-ip-address > < wildcard-mask > |

**Cách 1**

```
R(config)#access-list 1 deny 192.168.1.1 0.0.0.0
R(config)#access-list 1 deny host 192.168.1.1
R(config)#access-list 1 permit any
```

**Cách 2**

```
R(config)#ip access-list standard 1
R(config-std-nacl)#deny 192.168.1.1 0.0.0.0
R(config-std-nacl)#deny host 192.168.1.1
R(config-std-nacl)#permit any
```

## II. Extended access list

| Syntax |
|:---|
| access-list < acl-id (100-199) > < permit/deny > < protocol > < source-ip-address > < wildcard-mask > < destination-ip-address > < wildcard-mask > |

**Cách 1**

```
R(config)#access-list 100 deny icmp host 192.168.1.1 host 192.168.2.1
R(config)#access-list 100 deny tcp host 192.168.1.1 host 192.168.2.1 eq 80
R(config)#access-list 100 deny tcp host 192.168.1.1 host 192.168.2.1 eq 443
R(config)#access-list 100 permit tcp any any
```


**Cách 2**

```
R(config)#ip access-list extended 100
R(config-ext-nacl)#deny icmp host 192.168.1.1 host 192.168.2.1
R(config-ext-nacl)#deny tcp host 192.168.1.1 host 192.168.2.1 eq 80
R(config-ext-nacl)#deny tcp host 192.168.1.1 host 192.168.2.1 eq 443
R(config-ext-nacl)#permit tcp any any
```

## II. Áp cổng

| Syntax |
|:---|
| int < interface > <br/> ip access-group < acl-id > < in/out > |

```
int g0/0
ip access-group 1 out
```
