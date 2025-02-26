## Cum verific ca folosesc Quad9?

Cel mai simplu mod este de a deschide [on.quad9.net](https://on.quad9.net) în browserul dumneavoastră.

## Testul Protocolului folosit - Verificati pe ce Protocol primeste Quad9 interogarea dvs.

Confirmați ce protocol este folosit când Quad9 primește interogarea dvs. de DNS. Acest aspect este deosebit de important după setarea criptării DNS, cum ar fi DNS prin TLS sau DNS prin HTTPS, în sistemul de operare, router, redirectionare DNS.

Executați următoarea comandă și consultați răspunsurile posibile de mai jos:

=== "Windows (PowerShell/Terminal)"

    `Resolve-DnsName -Type txt proto.on.quad9.net.`
=== "MacOS/Linux/Unix (Terminal)"

    `dig +short txt proto.on.quad9.net.`

Răspunsuri posibile:

* do53-udp (53/UDP - Plaintext)
* do53-tcp (53/TCP - Plaintext)
* doh (443/TCP - DNS over HTTPS)
* dot (853/TCP - DNS over TLS)
* dnscrypt-udp (UDP - DNSCrypt)
* dnscrypt-tcp (TCP - DNSCrypt)

Dacă nu primiți un răspuns (NXDOMAIN), atunci Quad9 nu a fost utilizat pentru a efectua această interogare DNS.

## Identificarea unui bloc Quad9

Cea mai rapidă modalitate de a vedea dacă un domeniu este blocat la Quad9 este să utilizați pagina noastră [Blocked Domain Tester](https://quad9.net/result).

Atunci când Quad9 blochează un domeniu, răspunsul este `NXDOMAIN`. Răspunsul `NXDOMAIN` este returnat și atunci când un domeniu nu există. Pentru a face diferența între domeniile care nu există și domeniile care sunt blocate, setarea valorii `AUTHORITY` este diferită.  Atunci când primiți un `NXDOMAIN` cu `AUTHORITY: 0`, acesta este un blocaj din partea Quad9. Când primiți un `NXDOMAIN` *cu* `AUTHORITY: 1`, atunci este vorba despre un domeniu care nu există.

De asemenea, un domeniu nu va reuși să se rezolve dacă autentificarea DNSSEC eșuează, dar acest lucru va duce la codul `SERVFAIL` în loc de `NXDOMAIN`.


=== "Domeniu blocat"

    `dig @9.9.9.9 isitblocked.org | grep "status\|AUTHORITY"`
    ```
    ;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 29193
    ;; flags: qr rd ad; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1
    ```
=== "Domeniu inexistent"

    `dig @9.9.9.9 sfaisofnadgre.odafds | grep "status\|AUTHORITY:"`
    ```
    ;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 22595
    ;; flags: qr rd ra ad; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1
    ```
=== "Eșec DNSSEC"
    
    `dig @9.9.9.9 A brokendnssec.net +dnssec | grep status`
    ```
    ;; ->>HEADER<<- opcode: QUERY, status: SERVFAIL, id: 40999
    ```

## Detectarea redirecționării transparente a DNS (Hijack-uri)

Unii furnizori de servicii internet, cel mai adesea în Asia, Africa sau Orientul Mijlociu, redirecționează în mod transparent cererile DNS destinate serviciilor terțe de DNS, precum Quad9, către propriile expeditoare/servere DNS. Aceasta poate fi o încercare de a pune în aplicare politicile/legile locale sau pur și simplu de a crește rata HIT a cache-ului pe redirecționatoarele lor DNS (DNS Forwarders).

Puteți detecta o redirecționare DNS transparentă executând următoarea comandă din Prompt-ul de comandă sau din terminalul oricărui sistem de operare. Dacă răspunsul este altceva decât `resXXX.xxx.rrdns.pch.net`, atunci DNS este redirecționat transparent.

=== "Windows (PowerShell)"

    ```
    nslookup -q=txt -class=chaos id.server. 9.9.9.9 | Select-String "pch"
    ```

=== "MacOS/Linux/BSD (Terminal)"
    ```
    dig +short ch txt id.server. @9.9.9.9
    ```
Dacă rezultatul nu arată similar cu următorul sau nu există niciun rezultat, atunci DNS-ul este redirecționat transparent.

=== "Windows (PowerShell)"
    ```
    Non-authoritative answer:
    "res200.vie.rrdns.pch.net"
    ```

=== "MacOS/Linux/BSD (Terminal)"
    ```
    "res860.qfra3.rrdns.pch.net"
    ```
### ISP-ul meu redirecționează transparent DNS. Ce se întâmplă acum?

Vă rugăm să consultați Ghidurile noastre de configurare al căror titlu conține `(Encrypted)`. Prin utilizarea DNS criptat, redirecționarea DNS transparentă nu va fi posibilă.

## Ce este EDNS Client Subnet (ECS)?

Serviciul `9.9.9.11` al Quad9 suportă ECS.

EDNS Client Subnet (ECS) permite Quad9 să trimită o parte din adresa dvs. IP către serverele de nume autoritare, ceea ce ajută principalii furnizori de conținut (CDN), cum ar fi Google, Microsoft etc., să determine cu precizie geolocalizarea dvs.

ECS nu va avea niciun efect asupra locației Quad9 către care sunt trimise interogările dvs., ci doar asupra informațiilor pe care Quad9 le transmite către serverul de nume autoritativ și poate afecta adresa IP returnată. Quad9 utilizează adresarea anycast pentru a se asigura că sunteți direcționat către cea mai apropiată locație Quad9 disponibilă pentru dvs. indiferent dacă utilizați sau nu serviciul ECS.

Deoarece ECS nu joacă niciun rol în determinarea adresei către care sunt trimise interogările dvs., acesta nu are niciun efect pozitiv sau negativ asupra timpului de întoarcere (ping) către Quad9

ECS poate fi privit ca un compromis între confidențialitate și obținerea de conținut geospecific. O opțiune pentru utilizatorii preocupați de confidențialitate este să o lăsați dezactivată și să o activați numai dacă observați că un anumit domeniu nu vă oferă conținutul corect sau nu se încarcă deloc.

## Furnizori de rețea / Teste de scurgere DNS

Quad9 utilizează mai mulți furnizori de rețea în rețeaua noastră globală. Atunci când executați un test de scurgere DNS, este de așteptat să vedeți adrese IP deținute de următorii furnizori:

!!! nota "Instrument recomandat de testare a scurgerilor DNS"
    [dnscheck.tools](https://dnscheck.tools/)

* WoodyNet (AKA PCH.net)
* PCH.net
* i3D
* EdgeUno
* Equinix Metal (FKA: Packet, Packet.net, or Packethost)
* Path.net (Path Network)
* E-MAX (Bratislava, SK)

Aceste organizații sunt listate și pe pagina de Sponsori a site-ului Quad9: [quad9.net/about/sponsors](https://quad9.net/about/sponsors)

Dacă încercați doar să determinați dacă utilizați Quad9, puteți vizita [on.quad9.net](https://on.quad9.net) în loc să vă bazați pe un test de scurgere DNS. Cu toate acestea, un test de scurgere DNS poate fi util pentru a vă asigura că utilizați exclusiv Quad9, care este necesar pentru a vă asigura că toate solicitările DNS vor fi protejate de Quad9.