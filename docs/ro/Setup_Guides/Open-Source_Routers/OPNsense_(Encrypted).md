### Prezentare generală

OPNsense este un firewall open-source, utilizat atât în mediile comerciale, cât și în cele de consum.

OPNsense utilizează Unbound, care are încorporat suport DNS over TLS, configurarea fiind accesibilă în GUI.

!!! avertisment "Backup Time!"
    Înainte de a face modificări într-un mediu de producție, vă recomandăm [să faceți o copie de rezervă a configurației existente](https://docs.opnsense.org/manual/backups.html#backup)

### Instrucțiuni

* Navigați la `Servicii` -> `Unbound DNS` -> `DNS over TLS` în meniul din partea stângă
    * Faceți clic pe butonul +
        * Adăugați 4 intrări, folosind `dns.quad9.net` în câmpul **Verify CN**, și `853` în câmpul **Server Port:**.

Server IP: `9.9.9.9`
Server IP: `149.112.112.112`
Server IP: `2620:fe::fe`
Server IP: `2620:fe::9`

!!! avertisment "IPv6"
    Dacă rețeaua dvs. nu are IPv6, lucru pe care îl puteți testa aici, atunci adresele IPv6 nu ar trebui adăugate, deoarece pot duce la eșecul unui procent din cererile DNS.

* Faceți clic pe `Apply` pentru a salva modificările.

* Navigați la `System` -> `Settings` -> `General` în meniul din partea stângă.

* Dezactivați „Permiteți ca lista de servere DNS să fie suprascrisă de DHCP/PPP pe WAN
* Faceți clic pe `Save`
* Faceți clic pe `Apply` în partea de sus a paginii

### Verificarea configurației

Pentru a confirma că OPNsense trimite acum interogările dvs. prin DNS peste TLS, puteți rula o captură de pachete în linia de comandă, cum ar fi:

```
tcpdump -i em0 'port 853'
```

!!! notă
    Este posibil să trebuiască să ajustați numele interfeței de la em0 la cel al interfeței WAN a dispozitivului dumneavoastră.

De asemenea, puteți testa de pe un sistem macOS, Linux sau Windows care este conectat la acest router/firewall OPNsense.

[Obțineți asistență](https://quad9.net/support/contact){ .md-button .md-button--primary }
