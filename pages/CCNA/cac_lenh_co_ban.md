---
title: Các lệnh cơ bản
summary: "Một số lệnh cơ bản ở các mode"
sidebar: mydoc_sidebar
permalink: cac_lenh_co_ban.html
folder: CCNA
---

Các thành phần bên trong thiết bị cisco cơ bản gồm có:

* CPU: trung tâm xử lý
* RAM: bộ nhớ đệm
* Flash: bên trong lưu trữ hệ điều hành IOS (Internetwork Operating System), cấu hình configuration
* NVRAM (có ở router): lưu trữ cấu hình khởi động ban đầu (starup-config)
* ROM: lưu trữ chương trình POST (Power On Self Test) dùng để test phần cứng trước khi khởi động, ngoài ra còn có ROMMON, Bootstrap

Quy trình khởi động cơ bản: POST (ROM) -> Bootstrap (ROM) -> IOS (Flash) -> config (Flash/NVRAM)

## I. Các phím tắt và thông báo lỗi

|     |     |     |
| --- | --- | --- |
| Ctrl A | ahead | về đầu dòng lệnh |
| Ctrl E | end | về cuối dòng lệnh |
| Ctrl D | delete | xoá 1 ký tự phía sau |

|     |     |
| --- | --- |
| Ambigous command | từ gõ vào trùng nhiều lệnh |
| Incomplete command | lệnh chưa hoàn tất |
| Invalid command | giá trị nhập sai |
| Unknown command | lệnh không có hay không hỗ trợ trong mode này |

## II. Các lệnh cơ bản

1. Mode User

```
> enable
```

2. Mode Priviledge hay mode Enable

```
> enable
# exit
# show run
# show start
# copy run start | write
# erase start | write erase
# reload
# show ip int brief
```

3. Mode Global Configuration

```
# conf t
(config) # enable password 456
(config) # enable secret 789
(config) # no ip doamin-lookup
(config) # no ip doamin-lookup
(config) # no logging console
(config) # logging synchronous
```

4. Mode Sub Configuration

```
(config) # line console 0
(config-line) # pass 123
(config-line) # login
```

Ngoài ra còn nhiều lệnh khác nữa, trên đây là những lệnh thường gặp nhưng chưa đi sâu vào từng lệnh.
