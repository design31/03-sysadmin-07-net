# Домашнее задание к занятию "3.7. Компьютерные сети, лекция 2"

1. Проверьте список доступных сетевых интерфейсов на вашем компьютере. Какие команды есть для этого в Linux и в Windows?

В Windows для этого есть команда `ipconfig /all`:
```
C:\Users\y.kozlov>ipconfig /all

Настройка протокола IP для Windows

   Имя компьютера  . . . . . . . . . : XXX
   Основной DNS-суффикс  . . . . . . : XXX.local
   Тип узла. . . . . . . . . . . . . : Гибридный
   IP-маршрутизация включена . . . . : Нет
   WINS-прокси включен . . . . . . . : Нет
   Порядок просмотра суффиксов DNS . : XXX.local

Адаптер Ethernet Ethernet 4:

   DNS-суффикс подключения . . . . . :
   Описание. . . . . . . . . . . . . : Realtek PCIe GbE Family Controller
   Физический адрес. . . . . . . . . : F0-79-59-71-10-86
   DHCP включен. . . . . . . . . . . : Нет
   Автонастройка включена. . . . . . : Да
   IPv4-адрес. . . . . . . . . . . . : 192.168.5.174(Основной)
   Маска подсети . . . . . . . . . . : 255.255.255.0
   Основной шлюз. . . . . . . . . : 192.168.5.2
   DNS-серверы. . . . . . . . . . . : 192.168.5.XXX
                                       192.168.5.XXX
   NetBios через TCP/IP. . . . . . . . : Включен

Адаптер Ethernet VirtualBox Host-Only Network:

   DNS-суффикс подключения . . . . . :
   Описание. . . . . . . . . . . . . : VirtualBox Host-Only Ethernet Adapter
   Физический адрес. . . . . . . . . : 0A-00-27-00-00-02
   DHCP включен. . . . . . . . . . . : Нет
   Автонастройка включена. . . . . . : Да
   Локальный IPv6-адрес канала . . . : fe80::6c41:64a3:5525:48b1%2(Основной)
   IPv4-адрес. . . . . . . . . . . . : 192.168.56.1(Основной)
   Маска подсети . . . . . . . . . . : 255.255.255.0
   Основной шлюз. . . . . . . . . :
   IAID DHCPv6 . . . . . . . . . . . : 638189607
   DUID клиента DHCPv6 . . . . . . . : 00-01-00-01-29-04-9C-8B-F0-79-59-71-10-86
   DNS-серверы. . . . . . . . . . . : fec0:0:0:ffff::1%1
                                       fec0:0:0:ffff::2%1
                                       fec0:0:0:ffff::3%1
   NetBios через TCP/IP. . . . . . . . : Включен
```
В Linux ранее была команда ifconfig, сейчас больше используется `ip`:
```
us@ubuntu:~$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:81:0f:7d brd ff:ff:ff:ff:ff:ff
    inet 192.168.5.162/24 brd 192.168.5.255 scope global dynamic noprefixroute enp0s3
       valid_lft 27511sec preferred_lft 27511sec
    inet6 fe80::eb66:e6e5:f2c9:fa73/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
```
---

2. Какой протокол используется для распознавания соседа по сетевому интерфейсу? Какой пакет и команды есть в Linux для этого?

Для этого используется команда `lldpctl` из пакета `lldpd`:
```
us@ubuntu:~$ lldpctl |grep Interface
Interface:    enp0s3, via: LLDP, RID: 1, Time: 0 day, 00:05:10
Interface:    enp0s3, via: LLDP, RID: 2, Time: 0 day, 00:05:10
Interface:    enp0s3, via: LLDP, RID: 3, Time: 0 day, 00:05:09
Interface:    enp0s3, via: LLDP, RID: 4, Time: 0 day, 00:05:09
Interface:    enp0s3, via: LLDP, RID: 5, Time: 0 day, 00:05:08
Interface:    enp0s3, via: LLDP, RID: 6, Time: 0 day, 00:05:07
Interface:    enp0s3, via: LLDP, RID: 7, Time: 0 day, 00:05:06
Interface:    enp0s3, via: LLDP, RID: 8, Time: 0 day, 00:05:06
Interface:    enp0s3, via: LLDP, RID: 9, Time: 0 day, 00:05:05
Interface:    enp0s3, via: LLDP, RID: 10, Time: 0 day, 00:05:05
Interface:    enp0s3, via: LLDP, RID: 11, Time: 0 day, 00:05:05
Interface:    enp0s3, via: LLDP, RID: 12, Time: 0 day, 00:05:04
Interface:    enp0s3, via: LLDP, RID: 13, Time: 0 day, 00:05:04
Interface:    enp0s3, via: LLDP, RID: 14, Time: 0 day, 00:05:02
Interface:    enp0s3, via: LLDP, RID: 15, Time: 0 day, 00:04:58
Interface:    enp0s3, via: LLDP, RID: 16, Time: 0 day, 00:04:56
Interface:    enp0s3, via: LLDP, RID: 17, Time: 0 day, 00:04:55
Interface:    enp0s3, via: LLDP, RID: 18, Time: 0 day, 00:04:55
Interface:    enp0s3, via: LLDP, RID: 19, Time: 0 day, 00:04:55
Interface:    enp0s3, via: LLDP, RID: 20, Time: 0 day, 00:04:54
Interface:    enp0s3, via: LLDP, RID: 21, Time: 0 day, 00:04:52
Interface:    enp0s3, via: LLDP, RID: 22, Time: 0 day, 00:04:52
Interface:    enp0s3, via: LLDP, RID: 23, Time: 0 day, 00:04:51
Interface:    enp0s3, via: LLDP, RID: 24, Time: 0 day, 00:04:49
Interface:    enp0s3, via: LLDP, RID: 25, Time: 0 day, 00:04:49
Interface:    enp0s3, via: LLDP, RID: 26, Time: 0 day, 00:04:49
Interface:    enp0s3, via: LLDP, RID: 27, Time: 0 day, 00:04:49
Interface:    enp0s3, via: LLDP, RID: 28, Time: 0 day, 00:04:49
Interface:    enp0s3, via: LLDP, RID: 29, Time: 0 day, 00:04:49
Interface:    enp0s3, via: LLDP, RID: 30, Time: 0 day, 00:04:48
Interface:    enp0s3, via: LLDP, RID: 31, Time: 0 day, 00:04:48
Interface:    enp0s3, via: LLDP, RID: 32, Time: 0 day, 00:04:48
```
---

3. Какая технология используется для разделения L2 коммутатора на несколько виртуальных сетей? Какой пакет и команды есть в Linux для этого? Приведите пример конфига.


---

4. Какие типы агрегации интерфейсов есть в Linux? Какие опции есть для балансировки нагрузки? Приведите пример конфига.


---

5. Сколько IP адресов в сети с маской /29 ? Сколько /29 подсетей можно получить из сети с маской /24. Приведите несколько примеров /29 подсетей внутри сети 10.10.10.0/24.


---

6. Задача: вас попросили организовать стык между 2-мя организациями. Диапазоны 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16 уже заняты. Из какой подсети допустимо взять частные IP адреса? Маску выберите из расчета максимум 40-50 хостов внутри подсети.


---

7. Как проверить ARP таблицу в Linux, Windows? Как очистить ARP кеш полностью? Как из ARP таблицы удалить только один нужный IP?

