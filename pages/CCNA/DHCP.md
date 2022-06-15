
## I. Routing

```
R1(config)#ip route 192.168.2.0 255.255.255.0 10.0.0.2
R2(config)#ip route 192.168.1.0 255.255.255.0 10.0.0.1
```

## II. DHCP

|   |   |
|---|---|
| **ip dhcp pool** <name> | Khai báo tên pool |
| **network** <net-id> <subnet-mask> | Khai báo network sẽ cấp địa chỉ IP |
| default-router <ip-address> | Default gateway của các client |
| ip dhcp excluded-address <ip-address> <ip-address> | Địa chỉ IP loại trừ không cấp |
| service dhcp | Mở dịch vụ DHCP |

```
R(config)#ip dhcp pool <name>   // Khai báo tên pool
R(dhcp-config)#network 192.168.1.0 255.255.255.0   // Khai báo network sẽ cấp địa chỉ IP
R(dhcp-config)#default-router 192.168.1.254   // Default gateway của các client
R(dhcp-config)#exit
R(config)#ip dhcp excluded-address 192.168.1.1 192.168.1.10
R(config)#service dhcp 
```

```
R1(config)#ip dhcp pool 1
R1(dhcp-config)#network 192.168.1.0 255.255.255.0
R1(dhcp-config)#default-router 192.168.1.254
R1(dhcp-config)#exit

R1(config)#ip dhcp excluded-address 192.168.1.1 192.168.1.10

R1(config)#service dhcp 
```
