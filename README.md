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

Это VLAN. Для её использования в Ubuntu есть пакет vlan. Приведу пример временной настройки (до перезагрузки):
```
us@ubuntu:~$ sudo modprobe 8021q
us@ubuntu:~$ sudo apt-get install vlan
us@ubuntu:~$ sudo vconfig add enp0s3 9

Warning: vconfig is deprecated and might be removed in the future, please migrate to ip(route2) as soon as possible!

us@ubuntu:~$ sudo ip addr add 10.0.0.9/24 dev enp0s3.9
us@ubuntu:~$ sudo ip link set up enp0s3.9
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
       valid_lft 20026sec preferred_lft 20026sec
    inet6 fe80::eb66:e6e5:f2c9:fa73/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
3: enp0s3.9@enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default qlen 1000
    link/ether 08:00:27:81:0f:7d brd ff:ff:ff:ff:ff:ff
    inet 10.0.0.9/24 scope global enp0s3.9
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe81:f7d/64 scope link
       valid_lft forever preferred_lft forever
```
Здесь я добавил VLAN 9 на интерфейс enp0s3 и назначил ему новый IP адрес 10.0.0.9/24

---

4. Какие типы агрегации интерфейсов есть в Linux? Какие опции есть для балансировки нагрузки? Приведите пример конфига.


---

5. Сколько IP адресов в сети с маской /29 ? Сколько /29 подсетей можно получить из сети с маской /24. Приведите несколько примеров /29 подсетей внутри сети 10.10.10.0/24.

`ipcalc` о сети 10.10.10.0/29 говорит что:
```
us@ubuntu:~$ ipcalc 10.10.10.0/29
Address:   10.10.10.0           00001010.00001010.00001010.00000 000
Netmask:   255.255.255.248 = 29 11111111.11111111.11111111.11111 000
Wildcard:  0.0.0.7              00000000.00000000.00000000.00000 111
=>
Network:   10.10.10.0/29        00001010.00001010.00001010.00000 000
HostMin:   10.10.10.1           00001010.00001010.00001010.00000 001
HostMax:   10.10.10.6           00001010.00001010.00001010.00000 110
Broadcast: 10.10.10.7           00001010.00001010.00001010.00000 111
Hosts/Net: 6                     Class A, Private Internet
```
В этой подсети 8 адресов, включая адрес подсети и бродкаст. На хосты остается 6 адресов.

Посмотрим на 10.10.10.0/24:
```
us@ubuntu:~$ ipcalc 10.10.10.0/24
Address:   10.10.10.0           00001010.00001010.00001010. 00000000
Netmask:   255.255.255.0 = 24   11111111.11111111.11111111. 00000000
Wildcard:  0.0.0.255            00000000.00000000.00000000. 11111111
=>
Network:   10.10.10.0/24        00001010.00001010.00001010. 00000000
HostMin:   10.10.10.1           00001010.00001010.00001010. 00000001
HostMax:   10.10.10.254         00001010.00001010.00001010. 11111110
Broadcast: 10.10.10.255         00001010.00001010.00001010. 11111111
Hosts/Net: 254                   Class A, Private Internet
```
В `/24` подсети 256 адресов, значит, подсеть 10.10.10.0/24 можно разделить на 32 подсети 10.10.10.0/29
Подсети будут такими:
Network:   10.10.10.0/29 
Network:   10.10.10.8/29   
Network:   10.10.10.16/29 и т.д. до Network:   10.10.10.248/29 

---

6. Задача: вас попросили организовать стык между 2-мя организациями. Диапазоны 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16 уже заняты. Из какой подсети допустимо взять частные IP адреса? Маску выберите из расчета максимум 40-50 хостов внутри подсети.
 
 Есть ещё диапазон 100.64.0.0 — 100.127.255.255 с маской 255.192.0.0  (/10)
 Если нам необходимы подсети размером 50 хостов, можно посчитать так:
 ```
 us@ubuntu:~$ ipcalc 100.64.0.0/10 -s 50
Address:   100.64.0.0           01100100.01 000000.00000000.00000000
Netmask:   255.192.0.0 = 10     11111111.11 000000.00000000.00000000
Wildcard:  0.63.255.255         00000000.00 111111.11111111.11111111
=>
Network:   100.64.0.0/10        01100100.01 000000.00000000.00000000
HostMin:   100.64.0.1           01100100.01 000000.00000000.00000001
HostMax:   100.127.255.254      01100100.01 111111.11111111.11111110
Broadcast: 100.127.255.255      01100100.01 111111.11111111.11111111
Hosts/Net: 4194302               Class A

1. Requested size: 50 hosts
Netmask:   255.255.255.192 = 26 11111111.11111111.11111111.11 000000
Network:   100.64.0.0/26        01100100.01000000.00000000.00 000000
HostMin:   100.64.0.1           01100100.01000000.00000000.00 000001
HostMax:   100.64.0.62          01100100.01000000.00000000.00 111110
Broadcast: 100.64.0.63          01100100.01000000.00000000.00 111111
Hosts/Net: 62                    Class A

Needed size:  64 addresses.
Used network: 100.64.0.0/26
Unused:
100.64.0.64/26
100.64.0.128/25
100.64.1.0/24
100.64.2.0/23
100.64.4.0/22
100.64.8.0/21
100.64.16.0/20
100.64.32.0/19
100.64.64.0/18
100.64.128.0/17
100.65.0.0/16
100.66.0.0/15
100.68.0.0/14
100.72.0.0/13
100.80.0.0/12
100.96.0.0/11
```
 Т.е. оптимальным решением будут подсети /26 по 64 хоста.
 
---

7. Как проверить ARP таблицу в Linux, Windows? Как очистить ARP кеш полностью? Как из ARP таблицы удалить только один нужный IP?

Для Windows это команда `arp -a`:
```
C:\WINDOWS\system32>arp -a

Интерфейс: 192.168.56.1 --- 0x2
  адрес в Интернете      Физический адрес      Тип
  192.168.56.255        ff-ff-ff-ff-ff-ff     статический
  224.0.0.2             01-00-5e-00-00-02     статический
  224.0.0.7             01-00-5e-00-00-07     статический
  224.0.0.22            01-00-5e-00-00-16     статический
  224.0.0.251           01-00-5e-00-00-fb     статический
  224.0.0.252           01-00-5e-00-00-fc     статический
  224.0.1.60            01-00-5e-00-01-3c     статический
  224.0.1.75            01-00-5e-00-01-4b     статический
  238.238.238.238       01-00-5e-6e-ee-ee     статический
  239.192.152.143       01-00-5e-40-98-8f     статический
  239.254.127.63        01-00-5e-7e-7f-3f     статический
  239.255.255.250       01-00-5e-7f-ff-fa     статический
  255.255.255.255       ff-ff-ff-ff-ff-ff     статический

Интерфейс: 192.168.0.XXX --- 0xc
  адрес в Интернете      Физический адрес      Тип
  192.168.0.XXX          b4-2e-99-b7-6e-c4     динамический
  192.168.0.255         ff-ff-ff-ff-ff-ff     статический
  192.168.1.54          00-18-bc-00-79-12     динамический
  192.168.1.55          00-18-bc-00-78-5d     динамический
  192.168.1.56          00-18-bc-02-be-06     динамический
  192.168.1.60          00-18-bc-03-7e-a4     динамический
  ```
  Чтобы очистить ARP-кэш, необходимо выполнить команду: `netsh interface ip delete arpcache`  
  
  В Linux есть утилита `arp`  входящая в пакет `net-tools`. 
  Посмотреть все таблицы:
  ```
  us@ubuntu:~$ arp
Address                  HWtype  HWaddress           Flags Mask            Iface
192.168.5.254            ether   6c:3b:e5:07:8d:1a   C                     enp0s3
2floor_log.XXX.local     ether   30:8d:99:ac:2e:f9   C                     enp0s3
DC.XXX.local             ether   00:0c:29:83:5b:cb   C                     enp0s3
192.168.5.13             ether   00:17:c8:8e:3b:80   C                     enp0s3
192.168.5.197            ether   00:17:c8:9c:37:2e   C                     enp0s3
```
 Удалить один адрес из таблицы: 
 ```
 us@ubuntu:~$ sudo arp -d 192.168.5.254
[sudo] password for us:
us@ubuntu:~$ arp -i enp0s3
Address                  HWtype  HWaddress           Flags Mask            Iface
2floor_log.XXX.local     ether   30:8d:99:ac:2e:f9   C                     enp0s3
DC.XXX.local           ether   00:0c:29:83:5b:cb   C                     enp0s3
192.168.5.13             ether   00:17:c8:8e:3b:80   C                     enp0s3
192.168.5.197            ether   00:17:c8:9c:37:2e   C                     enp0s3
```
Удалить все записи можно командой:
```
root@ubuntu:/home/us# ip neigh flush all
root@ubuntu:/home/us# arp
Address                  HWtype  HWaddress           Flags Mask            Iface
hostname.XXX.local       ether   f0:79:59:71:10:86   C                     enp0s3
```
Или так:
```
root@ubuntu:/home/us# ip link set arp off dev enp0s3; ip link set arp on dev enp0s3
root@ubuntu:/home/us# arp
Address                  HWtype  HWaddress           Flags Mask            Iface
hostname.XXX.local       ether   f0:79:59:71:10:86   C                     enp0s3
```

---
