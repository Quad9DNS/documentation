## Prezentare generală

Cel mai simplu mod de a seta Quad9 pe întreaga rețea este prin setările routerului. Dacă preferați să configurați Quad9 pe un singur sistem, vă rugăm să urmați pașii de mai jos pentru a configura MX Linux 23 pentru a utiliza Quad9.

!!! avertisment „Firefox, VPN-uri”
    * **Firefox** este setat să utilizeze Cloudflare DNS în mod implicit în unele regiuni. Dacă utilizați Firefox, verificați dacă [acest lucru este dezactivat](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **VPN-urile** de obicei nu respectă setările DNS la nivel de sistem sau router. Dacă utilizați un VPN, configurați adresele IP ale Quad9 în setările `Custom DNS` ale clientului VPN. Consultați documentația furnizorului dvs. de VPN pentru informații suplimentare.

## Instrucțiuni

* Faceți clic dreapta pe pictograma Rețea/WiFi din bara de sistem din partea stângă a ecranului.
    * Selectați `Edit Connections`
        * Selectați tipul conexiunii (Wired sau Wi-Fi), apoi faceți clic pe butonul :gear: din partea de jos a ferestrei.

* Selectați fila `IPv4 Settings`.
    * Modificați `Method` la `Automatic (DHCP) addresses only`
        * În câmpul `DNS Servers`, adăugați: `9.9.9.9,149.112.112.112`
            * Faceți clic pe `Save`

## Verificarea configurației

Confirmați că utilizați Quad9 vizitând [on.quad9.net](https://on.quad9.net) în browserul dvs. preferat.

Întrebări? Probleme? Nu a funcționat? Contactați-ne!

[Obțineți asistență](https://quad9.net/support/contact){ .md-button .md-button--primary }
