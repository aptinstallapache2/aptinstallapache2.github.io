NAT - Network Address Translation

Loại
- NAT : IP
- PAT (Port Address Translation) : IP+Port

Cấu hình
- static: one to one
- dynamic 


R1
```
Default route
R1(config)#ip route 0.0.0.0 0.0.0.0 g0/1
```


NAT static
R1
```
R1(config)#ip nat inside source static 192.168.1.1 200.0.0.1
R1(config)#ip nat inside source static 192.168.1.2 100.0.0.1
R1(config)#int g0/0
R1(config-if)#ip nat inside
R1(config-if)#int g0/1
R1(config-if)#ip nat outside
```
R2
```
ip route 100.0.0.0 255.255.255.248 g0/1
```
