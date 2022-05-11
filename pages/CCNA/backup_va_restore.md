---
title: BACKUP VÀ RESTORE
summary: "Các lệnh backup và restore"
sidebar: mydoc_sidebar
permalink: telnet_ssh.html
folder: CCNA
---

Cấu hình xong thiết bị thì chúng ta nên backup để đề phòng khi sự cố xảy ra có thể restore thiết bị về trạng thái ban đầu trong thời gian nhanh nhất. Các thành phần trên thiết bị cisco cần backup:

* File **startup-config** chứa thông tin cấu hình
* Hệ điều hành **IOS**

## I. BACKUP

Backup sử dụng lệnh copy file đến TFTP server

Backup file **startup-config**

```
# copy start tftp
```

Backup file **IOS**

```
# copy flash tftp
```

## I. RESTORE

Restore ta tiến hành copy theo chiều ngược lại với backup

```
# copy tftp start
# copy tftp flash
```
