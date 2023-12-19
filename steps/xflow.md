interface fa0/0
ip address 3.7.2.254 255.255.255.0
no shutdown

interface loopback 1
ip address 200.3.7.1 255.255.255.0
no shutdown

interface loopback 2
ip address 100.3.7.1 255.255.255.0
no shutdown

ip dns server
ip domain-lookup
ip domain name tungusov.ru
ip host tungusov.ru 100.3.7.1

ip http server
ip http authentication local
username admin privilege 15 secret admin

ip dhcp pool pool1
network 3.7.2.0 255.255.255.0
default-router 3.7.2.254
dns-server 200.3.7.1
ip dhcp excluded-address 3.7.2.1 3.7.2.9

Запускаем астру
В графике запрашиваем соединение, он автоматически по DHCP выдаёт 10 адрес
ping tungusov.ru - тоже должен работать. Не сразу, но сработает

Запускаем винду 
В винде втыкаем сеть
IP 3.7.2.200 255.255.255.0
Шлюз 3.7.2.254
DNS 100.3.7.2

ip access-list extended ACL1
permit ip any any
monitor capture buffer tungusov_buf circular
monitor capture buffer tungusov_buf filter ACL1
monitor capture point ip cef tungusov_cap fastEthernet 0/0 both
monitor capture point associate tungusov_cap tungusov_buf
show monitor capture buffer tungusov_buf parameters

conf t
service sequence numbers
service timestamp
logging 3.7.2.200
no logging console

monitor capture point start tungusov_cap

Создаём трафик
Запускаем на W10 tftpd

monitor capture point stop tungusov_cap
monitor capture buffer tungusov_buf export tftp://3.7.2.200/R1.pcap

В папочку tftpd на C:// будет лежать трафик. ЕГо можно открыть в wireshark
С винды открывает http://100.3.7.1 с кредами admin admin


