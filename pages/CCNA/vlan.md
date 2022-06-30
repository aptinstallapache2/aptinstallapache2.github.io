## Chia vlan

```
SW1(config)#int g0/1
SW1(config-if)#switchport mode trunk
```

```
SW1(config)#vlan 101
SW1(config-vlan)#name Hanhchanh
SW1(config-vlan)#vlan 102
SW1(config-vlan)#name Kinhdoanh
SW1(config-vlan)#vlan 103
SW1(config-vlan)#name Ketoan

SW1(config)#vtp mode server
SW1(config)#vtp domain ABC
SW1(config)#vtp pass 123
```

```
SW1(config)#int range f0/1-2
SW1(config-if-range)#switchport mode access 
SW1(config-if-range)#switchport access vlan 101
```

## Inter Vlan
