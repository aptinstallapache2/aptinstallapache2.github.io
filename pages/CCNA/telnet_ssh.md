---
title: TELNET -SSH
summary: "Các lệnh cấu hình telnet và ssh"
sidebar: mydoc_sidebar
permalink: telnet_ssh.html
folder: CCNA
---

## I. TELNET

Telnet là giao thức đầu cuối ảo (virtual terminal) và là một phần của bộ giao thức TCP/IP. Telnet cho phép kết nối với thiết bị từ xa, thu thập thông tin, truyền lệnh và chạy chường trình. Telnet hoạt động trên port 23.

Virtual terminal (VTY) lines cho phép truy cập vào thiết bị thông qua các phiên kết nối. Khi người dùng kết nối vào thiết bị bằng VTY line, người đó đang kết nối vào một cổng ảo trên interface.

```
(config)# line vty 0 4 -> mở 5 phiên vty từ 0 đến 4 (có thể tăng hoặc giảm tuỳ theo số lượng cho phép kết nối)
(config-line)# pass [123]
(config-line)# login
```

Ngoài dùng pass để login, có thể dùng user pass thay thế.

```
(config)# user [admin] secret [456]
(config)# line vty 0 4
(config-line)# login local
```

## II. SSH

SSH là Secure Shell - là giao thức cho phép kết nối truyền dữ liệu bảo mật cao. SSH hoạt động trên port 22.

```
(config)# user [admin] secret [456]
(config)# ip domain-name box.local -> cần có do được sử dụng để tạo cặp key rsa
(config)# crypto key generate rsa -> sinh cặp key rsa
(config)# ip ssh version 2 -> sử dụng khi module cũ đang sử dụng ssh version cũ

(config)# line vty 0 4
(config-line)# login local
(config-line)# transport input ssh
```
