---
title: TELNET
summary: "Telnet"
sidebar: mydoc_sidebar
permalink: jn0_telnet.html
folder: JN0
---

## TELNET

Đặt hostname
```
root> configure
Entering configuration mode

root# set system host-name vMX1

[edit]
root# commit
commit complete

[edit]
root@vMX1#
```

Cài đặt telnet
```
[edit]
root@vMX1# set system services telnet

[edit]
root@vMX1# set system login user lab class super-user authentication plain-text-password
New password:
Retype new password:

[edit]
root@vMX1# commit
commit complete
```
