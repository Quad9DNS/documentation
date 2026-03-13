## Prezentare generală

DNS over TLS (DoT) și DNS over HTTPS (DoH) sunt acum suportate nativ în MacOS Big Sur și versiunile ulterioare.

Vă rugăm să urmați pașii de mai jos pentru a instala profilul DNS Quad9.

!!! eșecuri "VPN-uri, iCloud Private Relay, Little Snitch"
    Atunci când utilizați iCloud Private Relay, majoritatea clienților VPN sau Little Snitch, acesta nu va utiliza/respecta acest profil DNS.

    * **VPN**: nu urmați aceste instrucțiuni. În schimb, setați adresele IP ale Quad9 în setările `Custom DNS` ale clientului dvs. VPN. Consultați documentația clientului VPN pentru informații suplimentare.
   
    * **Apple Private Relay**: nu urmați aceste instrucțiuni. Apple Private Relay va utiliza propriile servere DNS la nivel de sistem, fără nicio modalitate de a le suprascrie

!!! avertisment "Firefox"
    * **Firefox** este setat să utilizeze DNS Cloudflare în mod implicit în unele regiuni. Dacă utilizați Firefox, verificați dacă [acest lucru este dezactivat](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).


## Alegerea DNS over TLS sau DNS over HTTPS

DNS over TLS este recomandat dacă dispozitivul se va conecta în principal la rețele Wi-Fi pe care le controlați sau la rețele corporative în care DNS over TLS este permis.

DNS over HTTPS este recomandat dacă dispozitivul se va conecta frecvent la Wi-Fi pentru oaspeți și/sau la rețele pe care nu le administrați, deoarece DoH nu este blocat la fel de frecvent de firewall-uri.

## Înainte de a începe

!!! nota "`nslookup` și `dig`"
    App Store, precum și comenzile `dig` și `nslookup` dintr-un `Terminal` nu utilizează DNS criptat. Acest lucru este intenționat.

!!! avertisment "DNS peste TLS"
    Dacă sunteți conectat la o rețea Wi-Fi care blochează DNS over TLS, ceea ce se poate întâmpla în cazul firewall-urilor de rețea restrictive, va trebui să dezactivați profilul sau să vă deconectați de la rețea pentru a recâștiga rezoluția DNS. Această soluție nu permite un comportament „fallback” necriptat. DNS over HTTPS este recomandat pentru majoritatea utilizatorilor

!!! avertisment "Acest profil va expira!"
    Aceste profiluri sunt valabile doar până când expiră, moment în care se vor dezactiva automat până la instalarea unui nou profil. Acest lucru este proiectat de Apple și nu există nicio modalitate de a-l evita.”

## Descărcați profilul
Descărcați unul dintre profilurile de aici direct utilizând Safari pe dispozitivul MacOS. Trebuie să utilizați Safari pentru a descărca fișierul.

* 9.9.9.9 (DNSSEC, Securizat)
    * [:fontawesome-solid-star:{ .heart } Recommended: HTTPS (.9) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `2fd22c5ca55ba2404a63f28a9cb4e25545194989a929895b3a689be232e62871`
    * [TLS (.9) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `56af33fe8d1e0f55d429f826fa9822a0a97a8aeb7ad28cca82b26536753d8132`

* 9.9.9.10 (Fără DNSSEC, fără blocarea amenințărilor)
    * [HTTPS (.10) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `ef18da540f7c30a3e9e0e7c4a40c3cde29791da0e02b9851f0195099383c901f`
    * [TLS (.10) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `6a76af77beace68de0a3ad3b4847eeff3f90eca60a2a7a01fd3063f2366f764c`

* 9.9.9.11 (DNSSEC, Securizat, cu ECS)
    * [HTTPS (.11) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_ECS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `1212594f9919783167338ea7d1797e8532e4b1426d58e0324983499c8c68dfc2`
    * [TLS (.11) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_ECS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `43a8da875650c899ce8ba6005040fca520951803bd9a02141ef7815cd164f785`

* 9.9.9.12 (Fără DNSSEC, fără blocarea amenințărilor, cu ECS)
    * [HTTPS (.12) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_ECS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `f5b2d174c7096b976af1c59df9c2423126ef59d96ae3fa2a8a3138907f910f2d`
    * [TLS (.12) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_ECS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `beb4610573f73d5fb524594530f07107000eb352b804f39ef84b226a8b75ab85`

## Instalare

* Navigați în folderul Descărcări și selectați profilul pe care tocmai l-ați descărcat.
    * Deschideți `Settings` > `Profile Downloaded` și selectați profilul Quad9 pe care l-ați deschis.
        * Faceți clic pe Install
            * Introduceți parola de acces a sistemului dvs.
!!! notă
    Veți primi un mesaj de avertizare care vă avertizează că traficul dvs. de rețea poate fi filtrat sau monitorizat de serverul DNS. În timp ce profilul Quad9 vă poate proteja dispozitivul prin filtrarea traficului potențial rău intenționat, niciunul din traficul dvs. nu va fi înregistrat de Quad9. Vă rugăm să consultați Politica noastră de confidențialitate pentru mai multe informații

* Selectați Install, apoi Install din nou.

* Profilul este acum instalat. Selectați `Done`

## Verificarea configurației

Pentru a confirma succesul instalării, vizitați [on.quad9.net](https://on.quad9.net)

Întrebări? Probleme? Nu a funcționat? Contactați-ne!

[Obțineți asistență](https://quad9.net/support/contact){ .md-button .md-button--primary }
