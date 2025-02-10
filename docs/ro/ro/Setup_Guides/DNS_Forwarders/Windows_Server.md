## Prezentare generală

Configurați Quad9 în Windows DNS Server pentru utilizarea în redirecționarea DNS.

!!! notă
    Înainte de a continua, vă rugăm să consultați articolul [Cele mai bune practici pentru redirecționarea DNS](https://docs.quad9.net/Quad9_For_Organizations/DNS_Forwarder_Best_Practices/).

## Instrucțiuni

* Deschideți `Server Manager` din meniul `Start`.
    * Din `Server Manager`, selectați `Tools` > `DNS`

* Din DNS Manager, faceți clic dreapta pe serverul dvs. și selectați `Properties`
    * Selectați fila `Forwarders` și apoi selectați `Edit`.
        * Adăugați următoarele adrese IP: `9.9.9.9`, `149.112.112.112`
        * Dacă rețeaua dvs. acceptă IPv6, adăugați și: `2620:fe::fe`, `2620:fe::9`
            * Faceți clic pe "Aplicare"

Întrebări? Probleme? Contactați-ne!

[Obțineți asistență](https://quad9.net/support/contact){ .md-button .md-button--primary }
