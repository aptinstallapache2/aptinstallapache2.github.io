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
