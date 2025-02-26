## Prezentare generală

Proiectul OpenWrt este un sistem de operare Linux destinat dispozitivelor integrate, care este adesea utilizat ca soluție open-source pentru routere și firewall-uri.

Acest ghid acoperă setarea Quad9 în setările DNS forwarder. Atunci când utilizați routerul OpenWrt ca server DNS, acesta va redirecționa solicitările DNS către Quad9.

!!! avertisment "Timp de rezervă!"
    Înainte de a face modificări într-un mediu de producție, vă recomandăm [să faceți o copie de rezervă a configurației existente](https://openwrt.org/docs/guide-user/troubleshooting/backup_restore)

## Instrucțiuni

* Conectați-vă la panoul de control LuCI, de obicei prin deschiderea `http://192.168.1.1` în browser.

* Navigați la `Network` -> `DHCP and DNS`
    * Setați `9.9.9.9` și `149.112.112.112`, sau adresele serviciului Quad9 preferat în câmpurile de introducere "DNS forwardings".

* Dacă rețeaua dvs. acceptă IPv6, puteți adăuga și 2620:fe::fe și 2620:fe::9, sau adresele IPv6 ale serviciului Quad9 preferat.

* Navigați la subpagina `Resolv and Hosts Files` și asigurați-vă că `Ignore resolv file` este `Enabled`.

* Faceți clic pe `Save & Apply` în partea de jos. Deoarece nu modificați setările DHCP, modificarea ar trebui să fie instantanee.

## Verificarea configurației

* Confirmați că utilizați Quad9 pe Linux, MacOS sau Windows.

[Obțineți asistență](https://quad9.net/support/contact){ .md-button .md-button--primary }
