## Prezentare generală

Pi-Hole este un redirecționator DNS popular, adesea utilizat în principal pentru blocarea domeniilor asociate în mod specific cu reclame și urmărire.

## Configurarea Pi-Hole

Pentru instrucțiuni detaliate de configurare a Pi-Hole în sine, consultați [Documentația oficială Pi-Hole] (https://docs.pi-hole.net/).

## Configurarea Quad9

Odată ce ați instalat Pi-Hole și puteți accesa panoul de administrare, Quad9 este deja una dintre opțiunile implicite.

* În panoul de administrare, navigați la `Settings` -> `DNS`
    * Bifați ambele căsuțe IPv4 de lângă Quad9 (filtered, DNSSEC)
        * Dacă rețeaua dvs. acceptă IPv6, se recomandă de asemenea bifarea ambelor casete IPv6. Dacă nu sunteți sigur dacă IPv6 este configurat în rețeaua dumneavoastră, puteți testa acest lucru aici: https://test-ipv6.com/

* Bifați/activați opțiunile:
    * `Never forward non-FQDNs` și `Never forward reverse lookups for private IP ranges` pentru a preveni trimiterea de interogări DNS fără răspuns către Quad9.
        * Faceți clic pe `Save` la sfârșit.

### Verificarea configurației

Odată ce Quad9 a fost configurat în Pi-Hole, puteți configura routerul sau un singur computer pentru a utiliza adresa IP a Pi-Hole ca server DNS. Dacă jurnalul de interogare este activat (Settings -> Privacy [fila]), ar trebui să vedeți Quad9 înregistrat în coloana Status:

De asemenea, puteți confirma dacă Quad9 este utilizat manual pe Linux, MacOS sau Windows.

### Domenii blocate

Domeniile care sunt blocate de Quad9 vor înregistra Blocked (extern, NXRA) în coloana Status din Query Log:

Întrebări? Probleme? Nu a funcționat? Contactați-ne!

[Obțineți asistență](https://quad9.net/support/contact){ .md-button .md-button--primary }
