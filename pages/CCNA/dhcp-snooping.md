---
title: DHCP SNOOPING
summary: "Cấu hình chống dhcp snooping và arp poisoning"
sidebar: mydoc_sidebar
permalink: dhcp-snooping.html
folder: CCNA
---

![image](./img/dhcp-snooping.png)

## I. DHCP Snooping

```
Switch(config)#ip dhcp snooping 
Switch(config)#ip dhcp snooping vlan 1
Switch(config)#no ip dhcp snooping information option 
Switch(config)#int fa0/24
Switch(config-if)#ip dhcp snooping trust 
```

## II. ARP Spoisoning

```
Switch(config)#ip arp inspection vlan 1
Switch(config)#ip dhcp snooping 
Switch(config)#ip dhcp snooping vlan 1
Switch(config)#no ip dhcp snooping information option 
Switch(config)#int fa0/24
Switch(config-if)#ip dhcp snooping trust 
Switch(config-if)#ip arp inspection trust 
```

