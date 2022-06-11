acl
ql gói qua cổng : áp vào cổng
ql telnet : áp vty
ql dịch vụ : áp dịch vụ tương ứng

2 loại standard (id 1-99)
extended (100-199)

ktra
theo thứ tự
gói tin ko thuộc phát biểu nào -> deny


access-list 1 deny 192.168.1.1 0.0.0.0
access-list 1 deny host 192.168.1.1

access-list 100 deny icmp host 192.168.1.1 host 192.168.2.1

int g0/0
ip access-group 1 out

https://gist.github.com/markandey/2225894
