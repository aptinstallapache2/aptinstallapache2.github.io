---
title: "Asterisk security: chạy với quyền non-root"
summary: "Các bước thêm user non-root cho Asterisk"
sidebar: mydoc_sidebar
permalink: asterisk_security_run_as_nonroot_user.html
folder: VoIP
---

## 1. Thêm user và group

```
$ sudo useradd asterisk
$ sudo passwd asterisk
```

## 2. Thay đổi permissions

```
$ sudo chown -R asterisk:asterisk /var/{lib,log,run,spool}/asterisk
$ sudo chown -R asterisk:asterisk /etc/asterisk
$ sudo chown asterisk:asterisk /usr/sbin/asterisk

# for 32-bit system
$ sudo chown -R asterisk:asterisk /usr/lib/asterisk

# for 64-bit system
$ sudo chown -R asterisk:asterisk /usr/lib64/asterisk
```

## 3. Cấu hình file asterisk.conf

```
$ sudo vim /etc/asterisk/asterisk.conf
...
[options]
runuser = asterisk
rungroup = asterisk
...
$ sudo systemctl restart asterisk
```

*(Source: https://hotkey404.com/asterisk-security-run-as-non-root-user/)*
