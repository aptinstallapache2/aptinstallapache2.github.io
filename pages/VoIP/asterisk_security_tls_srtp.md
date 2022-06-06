---
title: "Asterisk security: TLS và SRTP"
summary: "Các bước cấu hình TLS và SRTP Asterisk"
sidebar: mydoc_sidebar
permalink: asterisk_security_tls_srtp.html
folder: VoIP
---

Các bước sau đây được thực thi với quyền user `asterisk`

```
$ su asterisk
```

## 1. Tạo chứng chỉ

```
$ cd /usr/src/
$ cd asterisk-*/
$ bash contrib/scripts/ast_tls_cert -C pbx1.mycompany.local -O "My Company" -d /etc/asterisk/keys -b 2048
```

## 2. Cấu hình file sip.conf

```
$ vim /etc/asterisk/sip.conf
...
[general]
bindaddr=0.0.0.0
port=5061
transport=tls
encryption=yes
tlsprivatekey=/etc/asterisk/keys/asterisk.key
tlscertfile=/etc/asterisk/keys/asterisk.crt
tlsbindaddr=[::]:5061
tlsdontverifyserver=no
tlsclientmethod=tlsv1
tlsenable=yes
...

$ systemctl restart asterisk
```

*(Source: https://hotkey404.com/asterisk-security-using-self-signed-ssl-certificate-for-tls-registration/)*
