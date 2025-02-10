## Prezentare generală

Administrați DNS pentru o clădire, birou, afacere, ISP etc. și doriți să utilizați Quad 9. O alegere excelentă!

!!! notă

    Pentru ISP-urile sau organizațiile cu mai mult de 5.000 de utilizatori în spatele unui cache de redirecționare sau dacă vă așteptați la mai mult de 500 de interogări pe secundă de la o singură adresă IP de ieșire, vă rugăm să contactați [Quad9 Support](https://quad9.net/support/contact) cu detaliile implementării dvs., astfel încât să putem lucra împreună pentru a asigura o implementare fără probleme și de succes.

Redirecționatoarele de cache (Cache forwarders) și configurarea optimă a acestora sunt esențiale atunci când se trimit interogări în masă către Quad9 și sunt cele preferate comparativ cu atribuirea directă prin DHCP către utilizatorii finali în ceea ce privește:

### Performanță
Reducerea numărului de interogări care sunt redirecționate către Quad9, economisirea lățimii de bandă și oferirea unei experiențe mai rapide pentru utilizatorul final atunci când interogările sale se află deja în memoria cache a expeditorilor (forwarders' cache).


### Securitate
Activarea înregistrării interogărilor sau a unor tipuri de măsurători la nivel înalt este recomandată pentru a identifica posibile compromisuri de la anumite puncte finale sau clienți și este uneori impusă de legislația locală.

### Politica locală
Posibilitatea de a bloca sau de a analiza anumite FQDN la nivel de expeditor pune mai mult control în mâinile administratorului de rețea, fără a se baza exclusiv pe Quad9 pentru a bloca domeniile rău intenționate.

Atunci când setați Quad9 ca resolver recursiv în infrastructura dvs. și caching DNS forwarders, vă rugăm să luați în considerare următoarele bune practici.

### Exclusivitate

Deoarece redirecționatoarele DNS utilizează ordinea round-robin la redirecționarea interogărilor către o listă de servere DNS recursive, Quad9 trebuie să fie setat ca servere DNS recursive exclusive în redirecționatoarele dvs. Adăugarea unor servere DNS recursive suplimentare, altele decât Quad9, va duce la faptul că un procent din interogările DNS nu vor fi protejate de blocarea amenințărilor de către Quad9.

### Caching

Este imperativ ca redirecționatoarele DNS să fie configurate pentru a stoca în cache datele de răspuns pentru a evita interogările recursive excesive către Quad9 și pentru a oferi o rezoluție DNS semnificativ mai rapidă pentru dispozitivele din rețea.

Asigurați-vă că expeditoarele DNS au suficientă memorie sau spațiu pe disc alocat memoriei cache pentru a evita umplerea acesteia.

Cantitatea de memorie care ar trebui dedicată memoriei cache DNS variază foarte mult, de la megabytes la gigabytes, în funcție de cantitatea de cereri DNS provenite de la punctele terminale ale rețelei dvs.

=== "BIND"
    În mod implicit, Bind stochează memoria cache în memorie, astfel încât singura limitare este epuizarea memoriei disponibile în sistem.

    Pentru a verifica dimensiunea memoriei cache curente, puteți descărca memoria cache într-un fișier local și apoi să examinați dimensiunea fișierului, care va fi aproximativ cât de multă memorie este utilizată de cache:

    ```
    rndc dumpdb -all
    ```

    ```
    ls -alh /var/bind/
    ```
=== "dnsdist"
    Memoria cache este dezactivată în mod implicit, dar [poate fi activată pentru stocarea în memorie](https://dnsdist.org/guides/cache.html).
=== "Unbound"
    Dimensiunea cache-ului alocat este determinată de opțiunile msg-cache-size și rrset-cache-size din [fișierul unbound.conf](https://www.nlnetlabs.nl/documentation/unbound/unbound.conf/).

    Puteți verifica cantitatea de memorie pe care o utilizează în prezent memoria cache pentru a o compara cu dimensiunea memoriei cache pe care ați alocat-o în unbound.conf utilizând [comanda unbound-control](https://www.nlnetlabs.nl/documentation/unbound/unbound-control/) pentru a vizualiza statisticile pentru valorile mem.cache.rrset și mem.cache.message.

=== "Knot Resolver"
    Knot Resolver stochează memoria cache implicit pe disc, dar poate fi configurat să utilizeze memoria/tmpfs, backend-uri și să partajeze memoria cache între instanțe. Knot Resolver are [documentație excelentă despre toate aspectele legate de cache](https://knot-resolver.readthedocs.io/en/stable/daemon-bindings-cache.html).
=== "Windows DNS Server"

    Caching-ul în memorie poate fi configurat folosind applet-ul cmd `Set-DnsServerCache`.

    Utilizarea memoriei poate fi verificată cu ajutorul applet-ului cmd `Get-DnsServerStatistics`.

### Utilizați adresele IP Quad9 principale și secundare

Configurarea IP-ului primar *și* secundar al serviciului Quad9 dorit ajută la echilibrarea naturală a sarcinii interogărilor DNS în infrastructura Quad9.

### Utilizați IPv6

Dacă rețeaua dvs. este capabilă de IPv6, configurați, de asemenea, adresele IPv6 primară și secundară ale serviciului Quad9 dorit în redirecționatoarele DNS, ceea ce ajută la echilibrarea naturală a sarcinii interogărilor DNS în infrastructura Quad9.

În cazul în care IPv6 nu este utilizat, Quad9 vă încurajează insistent să investigați cum să îl activați în rețeaua dumneavoastră. Căile de rută IPv6 sunt adesea mai rapide comparativ cu căile IPv4, ceea ce duce la o șansă mai mare de succes la viteze mai mari, cu o redundanță mai bună.

### Adrese IP separate pentru fiecare Forwarder DNS

În mod ideal, fiecare expeditor DNS ar trebui să trimită și să primească interogări DNS către Quad9 folosind adrese IPv4 și IPv6 publice diferite, chiar dacă adresele se află în aceeași subrețea.

### Dezactivați validarea DNSSEC

Deoarece Quad9 efectuează deja validarea DNSSEC, activarea DNSSEC în redirecționator va cauza o dublare a procesului DNSSEC, reducând semnificativ performanța și putând cauza răspunsuri BOGUS false.


=== "dnsdist"
    Adăugați acest lucru în `dnsdist.conf` *deasupra* atribuirii grupului.
    ```
    if noDNSSECOnNOSEC then
      addAction(NetmaskGroupRule(nmgNOSEC, false), SetDisableValidationAction(), { name="R_NO_DS" })
    end
    ```
=== "Knot Resolver"
    Adăugați acest lucru la fișierul `kresd.conf` și reîncărcați/ reporniți serviciul `kresd`.
    ```
    -- turns off DNSSEC validation
    trust_anchors.remove('.')
    ```
=== "PowerDNS Recursor"
    În `recursor.conf`, dezactivați `dnssec` și reîncărcați/ reporniți `pdns-recursor`.
    ```
    dnssec=off
    ```
=== "Unbound"
    Comentați aceste linii în `unbound.conf` și reîncărcați/ reporniți unbound.
    ```
    trust-anchor-file:
    auto-trust-anchor-file:
    trust-anchor:
    trusted-keys-file:
    ```

### Dezactivarea minimizării QNAME

Minimizarea QNAME este o caracteristică de confidențialitate care este destinată a fi utilizată atunci când operați un rezolvator recursiv (Quad9), dar într-un expeditor DNS, aceasta nu oferă nicio îmbunătățire a confidențialității și reduce semnificativ performanța. [Ce este minimizarea QNAME?](https://www.isc.org/blogs/qname-minimization-and-privacy/)

=== "BIND"
    În secțiunea ```options {``` a fișierului named.conf, adăugați următoarea linie și reîncărcați/reporniți named/bind9.
    ```
    qname-minimization disabled;
    ```
=== "dnsdist"
    Minimizarea QNAME nu este acceptată în dnsdist. Nu este nimic de făcut aici.
=== "Unbound"
    Adăugați acest lucru în `unbound.conf` și reîncărcați/reporniți unbound. 
    ```
    qname-minimisation: no
    ```
=== "Knot Resolver"
    În fișierul `kresd.conf`, adăugați o politică pentru a dezactiva minimizarea QNAME și reporniți/reîncărcați serviciul `kresd`.
    ```
    policy.add(policy.all(policy.FLAGS('NO_MINIMIZE')))
    ```

Întrebări? Probleme? Contactați-ne!

[Obțineți asistență](https://quad9.net/support/contact){ .md-button .md-button--primary }
