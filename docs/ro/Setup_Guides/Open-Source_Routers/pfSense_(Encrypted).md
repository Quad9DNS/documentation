## Prezentare generală

pfSense este un firewall și un router open-source, utilizat atât în medii comerciale, cât și de consum.

pfSense are [documentație pentru DNS over TLS](https://docs.netgate.com/pfsense/en/latest/recipes/dns-over-tls.html), pe care recomandăm să o consultați în plus față de acest articol.

pfSense utilizează Unbound, care are încorporat suport DNS over TLS, configurația fiind accesibilă în interfața grafică.

!!! avertisment "Backup Time!"
    Înainte de a face modificări într-un mediu de producție, vă recomandăm [să faceți o copie de siguranță a configurației existente](https://docs.netgate.com/pfsense/en/latest/backup/configuration.html)

## Instrucțiuni

Navigați la `System` -> `General Setup` din meniul de sus.

* Faceți clic pe `Add DNS Server` până când există 4 rânduri de intrări disponibile.
* Adăugați adresele Quad9 IPv4 și IPv6 în câmpurile din stânga:
`9.9.9.9`,`149.112.112.112`,`2620:fe::fe`,`2620:fe::9`

!!! avertizare
    Dacă rețeaua dvs. nu are IPv6, lucru pe care îl puteți testa aici, atunci adresele IPv6 nu ar trebui adăugate, deoarece ar putea duce la eșecul unui procent din cererile DNS.

* Adăugați `dns.quad9.net` în toate câmpurile Hostname din dreapta.

Faceți clic pe "Save" în partea de jos a ecranului.

Navigați la `Services` -> `DNS Forwarder` din meniul de sus.
* Asigurați-vă că Enable DNS forwarder este dezactivat. Dacă este activat, dezactivați-l și faceți clic pe `Save` în partea de jos a paginii.

Navigați la `Services` -> `DNS Resolver` din meniul de sus.

* Derulați în jos până găsiți secțiunea vizibilă în următoarea captură de ecran.
* Dezactivați Enable DNSSEC Support dacă este activat.
!!! Notă "DNSSEC"
    DNSSEC este deja impus de Quad9, iar activarea DNSSEC la nivel de forwarder poate cauza eșecuri DNSSEC false.
* Activați `DNS Query Forwarding`
* Activați `Use SSL/TLS for outgoing DNS queries to Forwarding Servers`
* Faceți clic pe `Save` în partea de jos a ecranului.
* Faceți clic pe `Apply` Changes în partea de sus a ecranului pentru a aplica modificările salvate.

## Configurarea Veryify

Puteți confirma că pfSense trimite acum interogările dvs. prin DNS peste TLS utilizând Instrumentul de captare a pachetelor încorporat.

De asemenea, puteți efectua un test de pe un sistem macOS, Linux sau Windows din rețea.

[Obțineți asistență](https://quad9.net/support/contact){ .md-button .md-button--primary }
