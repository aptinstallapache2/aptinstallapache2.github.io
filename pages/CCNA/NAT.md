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


1.1 NAT static
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

1.2 NAT dynamic
R1
```
R1(config)#access-list 1 permit any
R1(config)#ip nat pool 1 100.0.0.1 100.0.0.2 netmask 255.0.0.0
R1(config)#ip nat inside source list 1 pool 1
```

2.2 PAT dynamic
```
R1(config)#access-list 1 permit any
R1(config)#ip nat pool 1 100.0.0.1 100.0.0.2 netmask 255.0.0.0
R1(config)#ip nat inside source list 1 pool 1 overload
```
c2
```
R1(config)#access-list 1 permit any
R1(config)#ip nat inside source list 1 int g0/1 overload
```

2.1 PAT static (NAT port forwarding)
```
R1(config)#ip nat inside source static tcp 192.168.1.1 80 200.0.0.1 80
```
