## Prezentare generală

IPFire este un firewall și un router open-source, utilizat atât în medii comerciale, cât și de consum.

IPFire utilizează Unbound, care are încorporat suport DNS over TLS, configurația fiind accesibilă în GUI.

Acest ghid de configurare a fost testat utilizând IPFire 2.27

!!! avertisment "Backup Time!"
    Înainte de a face modificări într-un mediu de producție, vă recomandăm [să faceți o copie de siguranță a configurației existente](https://wiki.ipfire.org/configuration/system/backup)

## Instrucțiuni

* Navigați la `System` -> `Domain Name System`
    * Sub `DNS Servers`, faceți clic pe `Add`
        * Treceți prin acest proces de două ori, câte una pentru fiecare adresă IP Quad9, unde numele de gazdă TLS va fi întotdeauna dns.quad9.net
            * IP address: `9.9.9.9`
            * IP address: `149.112.112.112`

* Use ISP-assigned DNS Servers: `Disabled`
* Protocol for DNS Queries: `TLS`
* Enable Safe Search: `Disabled`
* QNAME Minimisation: `Disabled`
* Faceți clic pe `Save`

## Verificarea configurației

### GUI

Navigați la `Status` -> `Net-Traffic` în meniul de sus și căutați o conexiune activă la `9.9.9.9` sau `149.112.112.112` prin portul 853 TCP

### CLI

* Conectați-vă la dispozitivul IPFire prin SSH
* Instalați pachetul tshark

```
pakfire -y install tshark
```

* Începeți o captură de pachete cu tshark pentru a filtra traficul DNS peste TLS:

```
tshark -i any 'port 853'
```

Dacă dispozitivul IPFire utilizează DNS over HTTPS pentru interogările DNS, veți vedea o ieșire ca aceasta:
```
1 0.000000000 192.168.1.150 → 9.9.9.9 TCP 76 37226 → 853 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 SACK_PERM=1 TSval=3103990808 TSecr=0 WS=512
2 0.006914259 9.9.9.9 → 192.168.1.150 TCP 76 853 → 37226 [SYN, ACK] Seq=0 Ack=1 Win=28960 Len=0 MSS=1460 TSval=2447463919 TSecr=3103990808 WS=256
3 0.006948874 192.168.1.150 → 9.9.9.9 TCP 68 37226 → 853 [ACK] Seq=1 Ack=1 Win=64512 Len=0 TSval=3103990815 TSecr=2447463919
4 0.007110658 192.168.1.150 → 9.9.9.9 TLSv1 387 Client Hello
5 0.013306457 9.9.9.9 → 192.168.1.150 TCP 68 853 → 37226 [ACK] Seq=1 Ack=320 Win=30208 Len=0 TSval=2447463926 TSecr=3103990815
6 0.013926633 9.9.9.9 → 192.168.1.150 TLSv1.3 2964 Server Hello, Change Cipher Spec, Application Data
7 0.013945067 192.168.1.150 → 9.9.9.9 TCP 68 37226 → 853 [ACK] Seq=320 Ack=2897 Win=62464 Len=0 TSval=3103990822 TSecr=2447463926
```

Întrebări? Probleme? Nu a funcționat? Contactați-ne!

[Obțineți asistență](https://quad9.net/support/contact){ .md-button .md-button--primary }
