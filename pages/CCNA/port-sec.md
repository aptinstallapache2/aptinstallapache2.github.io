
![image](https://user-images.githubusercontent.com/56266496/175776813-4e38ee44-8a42-481a-88a9-33f2a7d9729f.png)

```
SW1(config)#int range f0/1-24
SW1(config-if-range)#switchport mode access 
SW1(config-if-range)#switchport port-security
SW1(config-if-range)#switchport port-security max 1
SW1(config-if-range)#switchport port-security mac-address sticky 
SW1(config-if-range)#switchport port-security violation <protect/restrict/shutdown>
```
