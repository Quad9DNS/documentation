## Prezentare generală

Notă: Cei care mențin systemd-resolved subliniază faptul că această implementare DNS over TLS este în prezent o lucrare în curs de desfășurare. Puteți lua în considerare utilizarea Stubby în loc dacă întâmpinați probleme de performanță. Consultați aici pentru Ubuntu 18.04 / 20.04 + instrucțiuni Stubby.

Ubuntu 22.04 și Linux Mint 20.3 sau mai recente acceptă DNS over TLS în mod nativ în systemd-resolved, dar opțiunea nu este disponibilă în GUI.

!!! eroare
    Deși din punct de vedere tehnic acest lucru este acceptat și în Ubuntu *20.04*, nu recomandăm utilizarea acestei metode pentru 20.04, deoarece utilizează o versiune mai veche a systemd-resolve care are probleme. 

!!! eroare
    Opțiunea DNSSEC nu ar trebui să fie activată în systemd-resolved. Este extrem de eronată și nu ar face decât să dubleze procesul de validare DNSSEC pe care Quad9 îl efectuează deja, reducând semnificativ performanța.

!!! avertisment "Firefox, VPN-uri"
    * **Firefox** este setat să utilizeze Cloudflare DNS în mod implicit în unele regiuni. Dacă utilizați Firefox, verificați dacă [acest lucru este dezactivat](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **VPN-urile** de obicei nu respectă setările DNS la nivel de sistem sau router. Dacă utilizați un VPN, configurați adresele IP ale Quad9 în setările `Custom DNS` ale clientului VPN. Consultați documentația furnizorului dvs. de VPN pentru informații suplimentare.

## Instrucțiuni

* Configurați Quad9 în setările de rețea ([Ubuntu](https://docs.quad9.net/Setup_Guides/Linux_and_BSD/Ubuntu_20.04_and_22.04), [Linux Mint](https://docs.quad9.net/Setup_Guides/Linux_and_BSD/Linux_Mint_21.2)).

* Deschideți aplicația `Terminal` și copiați/lipiti aceste comenzi pentru a activa DNS over TLS. Când vi se solicită parola, introduceți-o și apăsați `Enter`.

```
sudo sed -i 's/#DNSOverTLS=no/DNSOverTLS=yes/g' /etc/systemd/resolved.conf
```

* Reporniți `systemd-resolvd` și `networking services` pentru a recunoaște modificările la fișier:

```
sudo systemctl restart systemd-resolved.service && sudo service network-manager restart
```
## Verificarea configurației

* Confirmați că DNS over TLS este utilizat deschizând aplicația `Terminal` și executând următoarea comandă, introducând parola și apăsând `Enter`:

```
$ dig +short txt proto.on.quad9.net.
```
Dacă răspunsul este `dot.`, atunci funcționează! Dacă răspunsul este `do53-udp.`, atunci încă se folosește text clar. Dacă nu există niciun răspuns, înseamnă că Quad9 nu a fost configurat probabil în `Network Settings`.

## Anulare

Dacă întâmpinați probleme sau doriți să anulați această modificare de configurare:

* Deschideți aplicația Terminal și copiați/lipiți aceste comenzi pentru a dezactiva DNS over TLS. Vi se va solicita parola.

```
sudo sed -i 's/DNSOverTLS=yes/#DNSOverTLS=no/g' /etc/systemd/resolved.conf
```

* Reporniți serviciile `systemd-resolvd` și `networking` pentru a recunoaște modificările aduse fișierului pe care tocmai le-am făcut:

```
sudo systemctl restart systemd-resolved.service && sudo service network-manager restart
```

Întrebări? Probleme? Nu a funcționat? Contactați-ne!

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
