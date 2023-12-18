[На главную](../index.md)

https://blog.sedicomm.com/2021/04/02/kak-nastroit-protokol-syslog-effektivnoe-zhurnalirovanie-sobytij-na-cisco-ios/

## Настройки syslog на маршрутизаторе

```
service timestamps log datetime
logging 192.168.1.2
logging trap 5
logging source-interface gi0/1
```

`show logging` - проверить

loggin trap ? 

## Не понял о чем это

```
В циске настраивать логгинг
conf t
logging ?

archive
log config
loggin enable
```