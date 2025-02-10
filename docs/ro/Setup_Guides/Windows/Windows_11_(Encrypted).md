## Prezentare generală

Cel mai simplu mod de a seta Quad9 pe întreaga rețea este prin setările routerului. Dacă preferați să setați Quad9 pe un dispozitiv Windows individual, vă rugăm să urmați pașii de mai jos pentru a configura Windows 11 pentru a utiliza Quad9.

!!! avertisment "Firefox, VPN-uri"
    * **Firefox** este setat să utilizeze Cloudflare DNS în mod implicit în unele regiuni. Dacă utilizați Firefox, verificați dacă [acest lucru este dezactivat](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **VPN-urile** de obicei nu respectă setările DNS la nivel de sistem sau router. Dacă utilizați un VPN, configurați adresele IP ale Quad9 în setările `DNS personalizat` ale clientului VPN. Consultați documentația furnizorului dvs. de VPN pentru informații suplimentare.
    

## Instrucțiuni

### IPv4

* Faceți clic dreapta pe pictograma rețea sau WiFi din bara de sistem și faceți clic stânga pe `Setări rețea și internet`

* Selectați `Ethernet` sau `WiFi`, în funcție de tipul de conexiune.

* Derulați în jos și faceți clic pe `Ediați` lângă `Alocarea serverului DNS`

* Efectuați următoarele modificări:
    * Schimbați `Automatic (DHCP)` la `Manual`
    * Treceți comutatorul `Activat` de la `IPv4` pentru a schimba serverul DNS
    * Introduceți în `DNS preferat`: 9.9.9.9
        * Setați `DNS prin HTTPS` la `Activat (șablon automat)`
    * Introduceți în `DNS alternativ`: 149.112.112.112
        * Setați `DNS prin HTTPS` la `Activat (șablon automat)`
!!! Notă
    Dacă utilizați un laptop care se deplasează către alte rețele care pot bloca DNS prin HTTPS, luați în considerare comutarea comutatorului `Revenire la text clar`.

* Faceți clic pe `Salvați`

### IPv6
Dacă utilizați IPv6, pe care îl puteți confirma aici: https://test-ipv6.com/, ar trebui, de asemenea, să defilați în jos și să configurați Quad9 pe IPv6.

* Efectuați următoarele modificări:
    * Treceți comutatorul `Activat` sub `IPv6` pentru a schimba serverul DNS
    * Introduceți în `DNS preferat`: 2620:fe::fe
        * Setați `DNS prin HTTPS` la `Activat (șablon automat)`
    * Introduceți în `DNS preferat`: 2620:fe::9
        * Setați `DNS prin HTTPS` la `Activat (șablon automat)`
!!! Notă
    Dacă Windows nu este configurat cu o adresă IPv6, configurarea unui server DNS IPv6 ar putea cauza eșecul rezoluției DNS.
    Dacă utilizați un laptop care se deplasează către alte rețele care pot bloca DNS prin HTTPS, luați în considerare activarea comutatorului `Revenire la text clar`.

* Faceți clic pe `Salvați` 

## Verificarea configurației

* Deschideți aplicația Terminal și executați această comandă:

```
Resolve-DnsName -Type txt proto.on.quad9.net.
```

La ieșire ar trebui să apară `doh.` (DNS over HTTPS) în secțiunea `NameHost` dacă ați setat Quad9 în setările de rețea și ați activat criptarea.

```
Name                           Type   TTL   Section    NameHost
----                           ----   ---   -------    --------
proto.on.quad9.net             CNAME  60    Answer     doh
```

Întrebări? Probleme? Nu a funcționat? Contactați-ne!

[Obțineți asistență](https://quad9.net/support/contact){ .md-button .md-button--primary }
