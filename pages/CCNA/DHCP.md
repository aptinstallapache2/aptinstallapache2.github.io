
## I. Routing

```
R1(config)#ip route 192.168.2.0 255.255.255.0 10.0.0.2
R2(config)#ip route 192.168.1.0 255.255.255.0 10.0.0.1
```

## II. DHCP

```
R(config)#ip dhcp pool <name> // Khai baos
R(dhcp-config)#network 192.168.1.0 255.255.255.0
R(dhcp-config)#default-router 192.168.1.254
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
