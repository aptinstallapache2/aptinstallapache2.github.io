---
title: "Asterisk security: SRTP"
summary: "Các bước cấu hình Asterisk dùng SRTP"
sidebar: mydoc_sidebar
permalink: asterisk_security_srtp.html
folder: VoIP
---

Các bước sau đây được thực thi với quyền user `asterisk`

```
$ su asterisk
```

```
$ sudo yum -y install openssl*
$ sudo yum -y install libsrtp

$ cd /usr/src/
$ cd asterisk-*/
$ sudo ./configure --libdir=/usr/lib64 --with-pjproject-bundled --with-jansson-bundled
$ sudo make
$ sudo make install

$ sudo systemctl restart asterisk
```
