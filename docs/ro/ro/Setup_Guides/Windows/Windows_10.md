## Prezentare generală

Cel mai simplu mod de a seta Quad9 pe întreaga rețea este prin setările routerului. Dacă preferați să setați Quad9 pe un dispozitiv Windows individual, vă rugăm să urmați pașii de mai jos pentru a configura Windows 10 pentru a utiliza Quad9.

!!! avertisment "Firefox, VPN-uri"
    * **Firefox** este setat să utilizeze Cloudflare DNS în mod implicit în unele regiuni. Dacă utilizați Firefox, verificați dacă [acest lucru este dezactivat](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **VPN-urile** de obicei nu respectă setările DNS la nivel de sistem sau router. Dacă utilizați un VPN, configurați adresele IP ale Quad9 în setările `Custom DNS` ale clientului VPN. Consultați documentația furnizorului dvs. de VPN pentru informații suplimentare.

## Instrucțiuni

### IPv4

* Faceți clic dreapta pe pictograma Rețea (Wired sau WiFi) din bara de sistem și faceți clic pe `Open Network & Internet Settings`.

* Faceți clic pe `Change adapter options`

* Selectați `Properties`.

* Selectați `Internet Protocol Version 4 (TCP/IPv4)`. Apoi, faceți clic pe `Properties`.

* Selectați `Use the following DNS server addresses`.
    * Introduceți: `9.9.9.9` în Preferred DNS Server
    * Introduceți: `149.112.112.112` în Server DNS alternativ.
* Faceți clic pe `OK`.

### IPv6

Dacă rețeaua dvs. acceptă IPv6, se recomandă, de asemenea, configurarea adreselor Quad9 IPv6. Dacă nu sunteți sigur dacă IPv6 este configurat în rețeaua dvs., puteți testa acest lucru aici: https://test-ipv6.com/

* Selectați Internet Protocol Version 6 (TCP/IPv6)
    * Faceți clic pe Properties (Proprietăți).

* Selectați `Use the following DNS server addresses`.
    * Introduceți: `2620:fe::fe` în Preferred DNS Server
    * Introduceți: `2620:fe::9` în Server DNS alternativ.
        * Faceți clic pe `OK`.

* Închideți toate ferestrele de configurare.

## Verificarea configurației

Confirmați că utilizați Quad9 vizitând [on.quad9.net](https://on.quad9.net) în browserul dvs. preferat.

Întrebări? Probleme? Nu a funcționat? Contactați-ne!

[Obțineți asistență](https://quad9.net/support/contact){ .md-button .md-button--primary }
