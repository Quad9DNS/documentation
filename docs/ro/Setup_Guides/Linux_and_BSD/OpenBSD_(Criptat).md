## Prezentare generală

Acest articol descrie modul de configurare și utilizare a Unbound pe OpenBSD pentru a trimite DNS criptat prin DNS over TLS către Quad9.

Acest lucru a fost testat utilizând OpenBSD 7.1.

!!! avertisment "Firefox, VPN-uri”
    * **Firefox** este setat să utilizeze Cloudflare DNS în mod implicit în unele regiuni. Dacă utilizați Firefox, verificați dacă [acest lucru este dezactivat](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **VPN-urile** de obicei nu respectă setările DNS la nivel de sistem sau router. Dacă utilizați un VPN, configurați adresele IP ale Quad9 în setările `Custom DNS` ale clientului VPN. Consultați documentația furnizorului dvs. de VPN pentru informații suplimentare.

!!! avertizare
    Unbound DNS este instalat în mod implicit pe instalațiile OpenBSD standard. Acesta este menit să acționeze ca un redirecționator DNS local, de cache, numai pentru mașina locală și nu este menit să acționeze ca un redirecționator DNS pentru alte dispozitive de rețea. Dacă doriți să rulați Unbound DNS pe OpenBSD în scopul de a rula un redirecționator DNS de caching care va fi utilizat de mai multe dispozitive din rețea, puteți modifica în mod corespunzător valorile de interfață și control al accesului din unbound.conf, care, în mod implicit, permit numai interogări DNS de la localhost.

## Instrucțiuni

Trebuie să fiți conectat ca utilizator root direct sau executând comanda `su` și introducând parola într-o sesiune Terminal.

* Copiați fișierul implicit unbound.conf și descărcați fișierul de înlocuire `unbound.conf`, care este pre-configurat pentru trimiterea interogărilor DNS către Quad9 prin DNS over TLS.

!!! notă
    Sunteți încurajat să descărcați și să inspectați fișierul unbound.conf într-un editor de text, care este atașat la acest articol, înainte de a-l descărca pe sistemul dvs. OpenBSD.

```
mv /var/unbound/etc/unbound.conf /var/unbound/etc/unbound.BAK && ftp -o /var/unbound/etc/unbound.conf https://docs.quad9.net/assets/conf/openbsd/unbound.conf
```

Opțional: Dacă rețeaua dvs. acceptă IPv6, deschideți fișierul /var/unbound/etc/unbound.conf pe OpenBSD cu editorul dvs. de text preferat și efectuați următoarele modificări, eliminând # (comentariu) înainte de începerea acestor linii.

**Înainte**

```
# do-ip6: no
# forward-addr: 2620:fe::fe@853#dns.quad9.net
# forward-addr: 2620:fe::9@853#dns.quad9.net
```

**După**

```
do-ip6: yes
forward-addr: 2620:fe::fe@853#dns.quad9.net
forward-addr: 2620:fe::9@853#dns.quad9.net
```

* Setați Unbound să pornească la pornirea sistemului și activați serviciul (executați aceste comenzi una câte una):

```
rcctl enable unbound
```
```
rcctl start unbound
```

## Verificarea configurației

Deschideți o sesiune Terminal separată/secundă la sistemul OpenBSD ca utilizator root și porniți o captură de pachete, filtrând pentru portul 853 (portul DNS prin TLS):
tcpdump -n 'port 853'

* La prima sesiune Terminal, asigurați-vă că Unbound poate răspunde la interogări DNS:
dig +short quad9.net @127.0.0.1

Rezultatul ar trebui să fie: 216.21.3.77

La a doua sesiune Terminal, tcpdump ar trebui să afișeze o ieșire ca aceasta, care confirmă că interogarea DNS a fost trimisă către Quad9 cu DNS over TLS:
```
tcpdump: listening on em0, link-type EN10MB
00:29:08.307240 192.168.1.194.42064 > 149.112.112.112.853: S 3620809840:3620809840(0) win 16384 <mss 1460,nop,nop,sackOK,nop,wscale 6,nop,nop,timestamp 495425124 0> (DF)
00:29:08.313467 149.112.112.112.853 > 192.168.1.194.42064: S 1684627303:1684627303(0) ack 3620809841 win 28960 <mss 1460,nop,nop,timestamp 3541989193 495425124,nop,wscale 8> (DF)
00:29:08.313559 192.168.1.194.42064 > 149.112.112.112.853: . ack 1 win 256 <nop,nop,timestamp 495425124 3541989193> (DF)
00:29:08.313895 192.168.1.194.42064 > 149.112.112.112.853: P 1:310(309) ack 1 win 256 <nop,nop,timestamp 495425124 3541989193> (DF)
00:29:08.319973 149.112.112.112.853 > 192.168.1.194.42064: . ack 310 win 118 <nop,nop,timestamp 3541989200 495425124> (DF)
00:29:08.320719 149.112.112.112.853 > 192.168.1.194.42064: . 1:1449(1448) ack 310 win 118 
```

Setați sistemul pentru a începe să utilizeze Unbound pentru DNS prin salvarea fișierului resolv.conf existent și setați 127.0.0.1 ca server DNS pentru sistem:
```
cp /etc/resolv.conf /etc/resolv.BAK && echo "nameserver 127.0.0.1" > /etc/resolv.conf
```

## Anulare

Dacă doriți să nu mai utilizați Unbound ca server DNS, restabiliți pur și simplu fișierul resolv.conf salvat:

```
mv /etc/resolv.BAK /etc/resolv.conf
```

Întrebări? Probleme? Nu a funcționat? Contactați-ne!

[Obțineți asistență](https://quad9.net/support/contact){ .md-button .md-button--primary }
