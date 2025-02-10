## Prezentare generală

Acest articol descrie modul de configurare a routerului MikroTik folosind RouterOS pentru a trimite interogări DNS criptate către Quad9 folosind DNS over HTTPS.

Este necesar RouterOS >=6.4.7. Aceste instrucțiuni au fost testate folosind RouterOS 7.1.3.

!!! avertisment "Backup Time!"
    Înainte de a face modificări într-un mediu de producție, vă recomandăm [să faceți o copie de siguranță a configurației existente](https://help.mikrotik.com/docs/display/ROS/Backup)

## Instrucțiuni

* Conectați-vă la interfața de administrare a routerului MikroTik prin SSH sau consolă. Numele de utilizator și parola vor fi aceleași ca în cazul utilizării Webfig (GUI).

* Pentru ca MikroTik să efectueze verificarea certificatului domeniului Quad9 DNS over HTTPS, trebuie să descărcați și să importați certificatul DigiCert Global Root CA.
    * Descărcați certificatul în routerul MikroTik:

```
/tool/fetch mode=https url="https://cacerts.digicert.com/DigiCertGlobalG3TLSECCSHA3842020CA1-1.crt.pem"
```

* Importați certificatul în magazinul local de certificate. Atunci când vi se solicită o frază de acces, apăsați Enter pentru nicio frază de acces:

```
/certificate/import file-name=DigiCertGlobalG3TLSECCSHA3842020CA1-1.crt.pem
```

Rezultatul ar trebui să fie:

```
passphrase: 
certificates-imported: 1
private-keys-imported: 0
files-imported: 1
decryption-failures: 0
keys-with-no-certificate: 0
```

* Intrați în Webfig (GUI) și navigați la `IP` -> `DNS` în meniul din partea stângă.
* În câmpul Servers, setați: `9.9.9.9`, `149.112.112.112`, `2620:fe::fe`, `2620:fe::9`

!!! avertizare

    Dacă rețeaua dvs. nu acceptă IPv6, atunci adresele IPv6 nu trebuie adăugate, deoarece pot duce la eșecul unui procent din cererile DNS. Nu sunteți sigur dacă aveți IPv6? [Testați aici](https://port.tools/ipv6-test/).

*  Use DoH Server: `https://dns.quad9.net/dns-query`
*  Verify DoH Certificate: `Enabled`
*  Allow Remote Requests: `Enabled`

!!! avertizare

    Nu uitați să configurați regulile de firewall pentru a preveni utilizarea acestei adrese IP nelocale ca server DNS.

8. Faceți clic pe **Apply** în partea de sus.

### Verificarea configurației

Pentru a confirma faptul că routerul MikroTik trimite interogări DNS către Quad9 utilizând DNS over HTTPS, puteți utiliza instrumentul Packet Sniffer pentru a filtra pachetele trimise către/de la adresele IP Quad9 utilizând portul 443 (HTTPS):

```
tool/sniffer/quick port=443 ip-address=9.9.9.9,149.112.112.112
```

Dacă interogările DNS trimise către routerul MikroTik sunt redirecționate către Quad9 folosind DNS over HTTPS, veți vedea orice ieșire.

```
Columns: INTERFACE, TIME, NUM, DIR, SRC-MAC, DST-MAC, SRC-ADDRESS, DST-ADDRESS, PROTOCOL, SIZE, CPU
INTERFACE TIME NUM DIR SRC-MAC DST-MAC SRC-ADDRESS DST-ADDRESS PROTOCOL SIZE CPU
ether1 6.886 5 <- 04:F0:21:45:C9:0C 08:00:27:7D:3B:33 9.9.9.9:443 (https) 192.168.1.222:59348 ip:tcp 66 0
ether1 6.887 6 <- 04:F0:21:45:C9:0C 08:00:27:7D:3B:33 9.9.9.9:443 (https) 192.168.1.222:59348 ip:tcp 1514 0
ether1 6.887 7 -> 08:00:27:7D:3B:33 04:F0:21:45:C9:0C 192.168.1.222:59348 9.9.9.9:443 (https) ip:tcp 66 0
ether1 6.887 8 <- 04:F0:21:45:C9:0C 08:00:27:7D:3B:33 9.9.9.9:443 (https) 192.168.1.222:59348 ip:tcp 1514 0
ether1 6.887 9 -> 08:00:27:7D:3B:33 04:F0:21:45:C9:0C 192.168.1.222:59348 9.9.9.9:443 (https) ip:tcp 66 0
```

Dacă nu aveți încă puncte finale care utilizează routerul MikroTik pentru DNS, puteți interoga manual routerul MikroTik pentru a facilita testarea și verificarea rezultatelor generate mai sus din Terminal (Linux/macOS) sau Command Prompt (Windows), înlocuind 192.168.1.1 cu adresa IP LAN a routerului MikroTik.

```
nslookup quad9.net 192.168.1.1
```

[Obțineți asistență](https://quad9.net/support/contact){ .md-button .md-button--primary }
