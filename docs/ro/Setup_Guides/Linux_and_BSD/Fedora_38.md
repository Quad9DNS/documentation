## Prezentare generală

Cel mai simplu mod de a configura Quad9 pe întreaga rețea este prin setările routerului. Dacă preferați să setați Quad9 pe un singur sistem, vă rugăm să urmați pașii de mai jos pentru a configura Fedora 38 pentru a utiliza Quad9.

!!! avertisment "Firefox, VPN-uri"
    * **Firefox** este setat să utilizeze Cloudflare DNS în mod implicit în unele regiuni. Dacă utilizați Firefox, verificați dacă [acest lucru este dezactivat](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **VPN-urile** de obicei nu respectă setările DNS la nivel de sistem sau router. Dacă utilizați un VPN, configurați adresele IP ale Quad9 în setările `Custom DNS` ale clientului VPN. Consultați documentația furnizorului dvs. de VPN pentru informații suplimentare.

## Instrucțiuni

### IPv4 

* Faceți clic pe pictograma `Network` sau `WiFi` din bara de sistem din colțul din dreapta sus al ecranului.
    * Faceți clic pe `>` de lângă conexiunea activă.
        * Selectați `Wired Settings` sau `Wireless Settings`.

* Faceți clic pe pictograma :gear: din dreptul conexiunii dvs.

* Faceți clic pe fila `IPv4`.
    * Dezactivați `Automatic DNS`
        * Introduceți adresele IP Quad9 ale serviciului dvs. preferat.

Mai multe adrese IP pot fi introduse în listă cu ajutorul virgulelor.

`9.9.9.9, 149.112.112.112`

* Dacă nu veți utiliza IPv6, faceți clic pe `Apply` pentru a finaliza procesul de configurare, apoi confirmați că utilizați Quad9.


### IPv6 (Opțional)

Dacă rețeaua dvs. acceptă IPv6, se recomandă și configurarea adreselor Quad9 IPv6. Dacă nu sunteți sigur dacă IPv6 este configurat în rețeaua dumneavoastră, puteți testa acest lucru aici: https://test-ipv6.com/


* Selectați fila `IPv6`.
    * Dezactivați `Automatic DNS`
        * Introduceți adresele IP Quad9 ale serviciului dvs. preferat.

Mai multe adrese IP pot fi introduse în listă cu ajutorul virgulelor.

`2620:fe::fe, 2620:fe::9`

* Faceți clic pe `Apply` pentru a finaliza procesul de configurare.

## Verificarea configurației

Confirmați că utilizați Quad9 vizitând [on.quad9.net](https://on.quad9.net) în browserul dvs. preferat.

Întrebări? Probleme? Nu a funcționat? Contactați-ne!

[Obțineți asistență](https://quad9.net/support/contact){ .md-button .md-button--primary }
