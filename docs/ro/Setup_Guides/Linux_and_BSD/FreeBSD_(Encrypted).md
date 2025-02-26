## Prezentare generală

Acest articol descrie modul de configurare și utilizare a serviciului „local_unbound” preinstalat de FreeBSD pentru a trimite DNS criptat prin DNS over TLS către Quad9.

Acest lucru a fost testat folosind FreeBSD 13.1, dar ar trebui să funcționeze și cu 12.X.

!!! avertisment "Firefox, VPN-uri"
    * **Firefox** este setat să utilizeze Cloudflare DNS în mod implicit în unele regiuni. Dacă utilizați Firefox, verificați dacă [acest lucru este dezactivat](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **VPN-urile** de obicei nu respectă setările DNS la nivel de sistem sau router. Dacă utilizați un VPN, configurați adresele IP ale Quad9 în setările `Custom DNS` ale clientului VPN. Consultați documentația furnizorului dvs. de VPN pentru informații suplimentare.

!!! avertisment
    FreeBSD, în mod implicit, instalează o instanță locală a Unbound DNS. Aceasta este menită să acționeze ca un redirecționator DNS local, pentru cache, doar pentru mașina locală, și nu este menită să acționeze ca un redirecționator DNS pentru alte dispozitive de rețea. Dacă doriți să rulați Unbound DNS pe FreeBSD în scopul de a rula un expeditor DNS de cache care va fi utilizat de mai multe dispozitive din rețea, FreeBSD recomandă instalarea pachetului dns/unbound. Aceste instrucțiuni sunt valabile doar pentru serviciul "local_unbound".

## Instrucțiuni

Veți avea nevoie de comanda sudo pentru a rula comenzile de mai jos. Alternativ, puteți utiliza pur și simplu comanda su pentru a deveni utilizator root și a executa aceste comenzi direct ca utilizator root, caz în care va trebui să eliminați "sudo" din toate comenzile de mai jos.

* Instalați comanda dig astfel încât să puteți testa dacă rezoluția DNS funcționează conform așteptărilor:

```
pkg install bind-tools
```

* Verificați dacă local_unbound este activat

```
sudo grep unbound /etc/rc.conf
```

Dacă se obține următorul rezultat, local_unbound este deja activat și puteți sări la secțiunea următoare:

```
local_unbound_enable="YES"
```

* Dacă nu există niciun rezultat după această comandă, atunci local_unbound trebuie să fie activat.
    * Spuneți sistemului că doriți să utilizați local_unbound:
```
echo 'local_unbound_enable="YES"' >> /etc/rc.conf
```

Apoi reporniți sistemul (da, într-adevăr):

```
reboot
```

* Enable local_unbound:

```
sudo local-unbound-setup
```

Rezultatul ar trebui să fie similar cu acesta, dar poate diferi ușor:

```
destination: 
Extracting forwarders from /etc/resolv.conf.
/var/unbound/forward.conf not modified
/var/unbound/lan-zones.conf not modified
/var/unbound/control.conf not modified
/var/unbound/unbound.conf not modified
local_unbound not running? (check /var/run/local_unbound.pid).
Starting local_unbound.
/etc/resolvconf.conf created
Original /etc/resolv.conf saved as /var/backups/resolv.conf.20220625.200835
```

Configurarea local_unbound pentru DNS prin TLS către Quad9

Această comandă va salva fișierele de configurare implicite, va descărca fișierele de configurare modificate din atașamentul acestui articol și va reporni serviciul local_unbound.

```
sudo mv /var/unbound/forward.conf /var/unbound/forward-ORIG.conf && sudo mv /var/unbound/unbound.conf /var/unbound/unbound-ORIG.conf && sudo fetch -o /var/unbound/unbound.conf https://docs.quad9.net/assets/conf/freebsd/unbound.conf && sudo fetch -o /var/unbound/forward.conf https://docs.quad9.net/assets/conf/freebsd/forward.conf && sudo service local_unbound restart
```

Aceste fișiere sunt configurate implicit pentru serviciul nostru 9.9.9.9, fără IPv6. Dacă doriți să utilizați în schimb serviciul .10 sau .11 și/sau să activați IPv6, deschideți fișierul `/var/unbound/forward.conf` și de-comentați/comentați liniile corespunzătoare.

## Verificarea configurației

Veți avea nevoie de două sesiuni/ferestre de terminal

În prima sesiune, porniți o captură de pachete pentru a filtra traficul DNS over TLS:

```
sudo tcpdump -n 'port 853'
```

În a doua sesiune, generați câteva căutări DNS:

```
dig +short quad9.net && dig +short www.quad9.net && dig +short zombo.com
```

Reveniți la prima sesiune. Dacă vedeți vreo ieșire, sistemul dvs. utilizează acum DNS peste TLS pentru a trimite DNS criptat către Quad9:

```
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on em0, link-type EN10MB (Ethernet), capture size 262144 bytes
20:30:21.004625 IP 192.168.1.118.29017 > 149.112.112.112.853: Flags [S], seq 255439876, win 65535, options [mss 1460,nop,wscale 6,sackOK,TS val 2441683586 ecr 0], length 0
20:30:21.011088 IP 149.112.112.112.853 > 192.168.1.118.29017: Flags [S.], seq 838572319, ack 255439877, win 28960, options [mss 1460,nop,nop,TS val 3171725219 ecr 2441683586,nop,wscale 8], length 0
20:30:21.011140 IP 192.168.1.118.29017 > 149.112.112.112.853: Flags [.], ack 1, win 1027, options [nop,nop,TS val 2441683592 ecr 3171725219], length 0
20:30:21.011628 IP 192.168.1.118.29017 > 149.112.112.112.853: Flags [P.], seq 1:294, ack 1, win 1027, options [nop,nop,TS val 2441683592 ecr 3171725219], length 293
20:30:21.017885 IP 149.112.112.112.853 > 192.168.1.118.29017: Flags [.], ack 294, win 118, options [nop,nop,TS val 3171725226 ecr 2441683592], length 0
20:30:21.018447 IP 149.112.112.112.853 > 192.168.1.118.29017: Flags [.], seq 1:1449, ack 294, win 118, options [nop,nop,TS val 3171725227 ecr 2441683592], length 1448
20:30:21.018453 IP 149.112.112.112.853 > 192.168.1.118.29017: Flags [.], seq 1449:2897, ack 294, win 118, options [nop,nop,TS val 3171725227 ecr 2441683592], length 1448
```

## Undo

Pentru a anula modificările de configurare la local_unbound, pur și simplu executați această comandă pentru a restabili fișierele originale și a reporni local_unbound:

```
sudo mv /var/unbound/forward-ORIG.conf /var/unbound/forward.conf && sudo mv /var/unbound/unbound-ORIG.conf /var/unbound/unbound.conf && sudo service local_unbound restart
```

Întrebări? Probleme? Nu a funcționat? Contactați-ne!

[Obțineți asistență](https://quad9.net/support/contact){ .md-button .md-button--primary }
