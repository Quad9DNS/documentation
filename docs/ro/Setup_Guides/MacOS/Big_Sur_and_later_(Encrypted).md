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
    * [:fontawesome-solid-star:{ .heart } Recommended: HTTPS (.9) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `b240f046a16f7d0e5df6458f5121221c4f118bf4d415cd8cce47d10b6fd46d36`
    * [TLS (.9) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `d132d71447bc3b43e371a86533e4d12fa46a4690a63abf77b2ceae72a1b3cef3`

* 9.9.9.10 (Fără DNSSEC, fără blocarea amenințărilor)
    * [HTTPS (.10) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `42cb9445417dc81ced18c33d943c23559a81afb018d440bf465bb0635a44bb66`
    * [TLS (.10) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `86588f6d2dac42d03b155c7f557b4dd05b354059736aaa4ec8f3ef4d3ca2548e`

* 9.9.9.11 (DNSSEC, Securizat, cu ECS)
    * [HTTPS (.11) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_ECS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `38c52f0755c4ec053c685e1ebf3b9956841a81373df2cc2e9dc962a418ac6993`
    * [TLS (.11) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_ECS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `abf69de093831cf8c4d644d234a3a594d13026415533ad1bb2b9f1540f307a46`

* 9.9.9.12 (Fără DNSSEC, fără blocarea amenințărilor, cu ECS)
    * [HTTPS (.12) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_ECS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `eccb63252a1cd6726d42a1d72c58e11503cf06a0de6977d2472386f9cc88d9d8`
    * [TLS (.12) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_ECS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `0b01df454c9e4ee7f39b0a79e63920c6fa6e44f1fe17c0064bb8da6ce68bcb04`

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
