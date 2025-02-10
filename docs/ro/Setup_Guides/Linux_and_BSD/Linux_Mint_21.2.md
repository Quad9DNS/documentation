## Prezentare generală

Cel mai simplu mod de a seta Quad9 pe întreaga rețea este prin setările routerului. Dacă preferați să setați Quad9 pe un singur sistem, vă rugăm să urmați pașii de mai jos pentru a configura Linux Mint pentru a utiliza Quad9.

!!! avertisment "Firefox, VPN-uri"
    * **Firefox** este setat să utilizeze Cloudflare DNS în mod implicit în unele regiuni. Dacă utilizați Firefox, verificați dacă [acest lucru este dezactivat](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **VPN-urile** de obicei nu respectă setările DNS la nivel de sistem sau router. Dacă utilizați un VPN, configurați adresele IP ale Quad9 în setările `Custom DNS` ale clientului VPN. Consultați documentația furnizorului dvs. de VPN pentru informații suplimentare.

## Instrucțiuni 

* Faceți clic pe pictograma `Network` sau `Wi-Fi` din bara de sistem din colțul din dreapta jos.
    * Faceți clic pe `Network Settings`
        * Faceți clic pe pictograma :gear: din colțul din dreapta jos al ferestrei de dialog.
### IPv4

* Selectați `IPv4` în meniul din partea stângă.
    * În secțiunea `DNS`:
        * Dezactivați `Automatic`
            * Faceți clic pe butonul :plus: pentru a adăuga un al doilea câmp `Server`.
                * Introduceți `9.9.9.9` în primul câmp `Server`, iar `149.112.112.112` în al doilea.
                    * Faceți clic pe `Apply`

## Verificarea configurației

Confirmați că utilizați Quad9 vizitând [on.quad9.net](https://on.quad9.net) în browserul dvs. preferat.

Întrebări? Probleme? Nu a funcționat? Contactați-ne!

[Obțineți asistență](https://quad9.net/support/contact){ .md-button .md-button--primary }
