---
title: CDP/LLDP
summary: "Giao thức thu thập thông tin các thiết bị láng giềng"
sidebar: mydoc_sidebar
permalink: cdp_lldp.html
folder: CCNA
---

## I. CDP

**Cisco Discovery Protocol (CDP)** là giao thức riêng của Cisco dùng để thu thập thông tin về neighbor (láng giềng). Sử dụng CDP, ta có thể biết được thông tin phần cứng của các thiết bị gần kề, thông tin này hữu ích trong xử lý sự cố hay kiểm soả thiết bị trong mạng.

```
# show cdp
# show cdp neighbors
# show cdp neighbors detail
# show cdp entry *
# show cdp interface
```

Bật tắt CDP:

```
(config)# no cdp run
(config)# cdp run
(config)# interface e0
(config-if)# no cdp enable
```

## II. LLDP

Tương tự CDP.

```
# lldp run
# show lldp neighbors
```

