[На главную](../index.md)

## Настройка DHCP пула на роутере
```
R1> ip dhcp pool pool1
> network 3.7.2.0 255.255.255.0
> default-router 3.7.2.254
> dns-server 200.3.7.1
> ip dhcp excluded-address 3.7.2.1 3.7.2.9
```