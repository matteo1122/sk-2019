Zadanie 1
---------

![zadanie 1](zadanie-1.svg)

1. Zaprojektuj oraz przygotuj prototyp rozwiązania z wykorzystaniem oprogramowania ``VirtualBox`` lub podobnego. 
Zaproponuj rozwiązanie spełniające poniższe wymagania:
   * Usługodawca zapewnia domunikację z siecią internet poprzez interfejs ``eth0`` ``PC0``
   * Zapewnij komunikację z siecią internet na poziomie ``LAN1`` oraz ``LAN2``
   * Dokonaj takiego podziału sieci o adresie ``172.22.128.0/17`` aby w ``LAN1`` można było zaadresować ``500`` adresów natomiast w LAN2 ``5000`` adresów    
   * Przygotuj dokumentację powyższej architektury w formie graficznej w programie ``DIA``
 
Rozwiązanie

PC0  
-------------------
|  interfejs   | adres  |
|:-------------| :------| 
| eth0 | usługodawca zapewnia komunikację z siecią internet  |
| eth1 | 172.22.160.1/23  |
| eth2 | 172.22.128.1/19  |

PC1  
----------------
|  interfejs   | adres  |
|:-------------| :------| 
|eth0|172.22.160.2/23|

PC2  
------------------
|  interfejs   | adres  |
|:-------------| :------| 
| eth0 | 172.22.128.2/19 |

Ustawienie adresów IP: ``ip addr add (adres IP) dev (interfejs enp0s3/8/9)``  
Włączenie interfejsu: ``ip link set (interfejs) up``  
Włączenie forwardingu na serwerze: ``sysctl -w net.ipv4.ip_forward=1``  
Dodawanie trasy routingu dla hostów: ``ip route add default (adres interfejsu serwera w danej sieci)``  
Udostępnienie internetu dla podsieci: ``iptables -t nat -A POSTROUTING -o (interfejs zewnętrzny) -j MASQUERADE``  
