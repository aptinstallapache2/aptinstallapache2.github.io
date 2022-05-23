---
title: Cài đặt Asterisk 16 trên Oracle linux 8
summary: "Các bước cài đặt Asterisk 16.26.1 stable trên hệ điều hành Oracle linux 8.6"
sidebar: mydoc_sidebar
permalink: install_asterisk_16_on_oracle_linux_8.html
folder: VoIP
---

Disable SELINUX

```
$ sudo sed -i 's/\(^SELINUX=\).*/\SELINUX=disabled/' /etc/selinux/config
$ sudo reboot
```

Cài đặt các package cần thiết

```
$ sudo yum -y install epel-release
$ sudo yum group -y install "Development Tools"
$ sudo yum -y install git wget net-tools sqlite-devel psmisc libtermcap-devel newt-devel libxml2-devel libtiff-devel gtk2-devel libtool subversion kernel-devel crontabs cronie-anacron make openssl-devel gcc gcc-c++ ncurses-devel libuuid-devel libedit libedit-devel
```

* Nếu không cài đặt được libedit-devel thì dùng rpm để cài đặt

```
Unable to find a match: libedit-devel
$ sudo rpm -i https://vault.centos.org/centos/8/PowerTools/x86_64/os/Packages/libedit-devel-3.1-23.20170329cvs.el8.x86_64.rpm
```

Cài đặt Jansson

```
$ cd /usr/src/
$ sudo git clone https://github.com/akheron/jansson.git
$ cd jansson
$ sudo autoreconf -i
$ sudo ./configure --prefix=/usr/
$ sudo make && sudo make install
```

Cài đặt PJSIP

```
$ cd /usr/src/
$ sudo git clone https://github.com/pjsip/pjproject.git
$ cd pjproject
$ sudo ./configure CFLAGS="-DNDEBUG -DPJ_HAS_IPV6=1" --prefix=/usr --libdir=/usr/lib64 --enable-shared --disable-video --disable-sound --disable-opencore-amr
$ sudo make dep
$ sudo make
$ sudo make install
$ sudo ldconfig
```

Cài đặt Asterisk

```
$ cd /usr/src/
$ sudo wget http://downloads.asterisk.org/pub/telephony/asterisk/asterisk-16-current.tar.gz
$ sudo tar xvfz asterisk-16-current.tar.gz
$ sudo rm -f asterisk-16-current.tar.gz
$ cd asterisk-16*/
$ sudo ./configure --libdir=/usr/lib64
$ sudo make menuselect
$ sudo contrib/scripts/get_mp3_source.sh
$ sudo ./contrib/scripts/install_prereq install
$ sudo make
$ sudo make install
$ sudo make samples
$ sudo make config
$ sudo ldconfig
```

Khởi động asterisk service

```
$ cd /usr/src/
$ cd asterisk-16*/
$ cd contrib/systemd/
$ sudo systemctl restart asterisk
```

Kết quả, chạy asterisk

```
$ sudo asterisk -rvv
*CLI>
```
