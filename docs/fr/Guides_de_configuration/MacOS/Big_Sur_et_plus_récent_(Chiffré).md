## Aperçu

DNS over TLS (DoT) et DNS over HTTPS (DoH) sont désormais pris en charge sur MacOS Big Sur et les versions ultérieures.

Veuillez suivre les étapes ci-dessous pour installer le profil DNS Quad9.

!!! failure "Les VPNs, iCloud Private Relay, Little Snitch"
    Quand vous utilisez iCloud Private Relay, la plupart des clients VPN, ou encore Little Snitch, il n'utilisera pas ce profil DNS..

	* **Les VPNs** ne respectent généralement pas les paramètres DNS du système ou du routeur. Si vous utilisez un VPN, configurez les adresses IP de Quad9 dans les paramètres « DNS personnalisé » de votre client VPN. Reportez-vous à la documentation de votre fournisseur VPN pour plus d'informations.
   
    * **Apple Private Relay**: Apple Private Relay doit être désactivé.

!!! warning "Firefox"
    * **Firefox** est configuré pour utiliser Cloudflare DNS par défaut dans certaines régions. Si vous utilisez Firefox assurez vous que cette fonctionalité [soit desactivée](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).


## Choisir DNS over TLS ou DNS over HTTPS

DNS over TLS est recommandé si l'appareil se connecte principalement aux réseaux Wi-Fi que vous contrôlez ou aux réseaux d'entreprise où DNS over TLS est autorisé.

DNS over HTTPS est recommandé si l'appareil se connecte fréquemment au Wi-Fi invité et/ou aux réseaux que vous n'administrez pas, car DoH n'est pas aussi souvent bloqué sur les pare-feu (firewalls).

## Avant de commencer

!!! note "`nslookup` et `dig`"
    L'App Store, ainsi que les commandes `dig` et `nslookup` dans un `Terminal` n'utilisent pas de DNS chiffré. Ils sont conçus comme ça .

!!! warning "DNS over TLS"
    Si vous êtes connecté à un réseau Wi-Fi qui bloque DNS over TLS, ce qui peut se produire sur des pare-feu réseau restrictifs, vous devrez désactiver le profil ou vous déconnecter du réseau pour retrouver la résolution DNS. Cette solution ne permet pas un comportement de « secours » non chiffré. DNS over HTTPS est recommandé pour la plupart des utilisateurs.

!!! warning "This profile will expire!"
    Ces profils ne sont valides que jusqu'à leur expiration, auquel cas ils seront automatiquement désactivés jusqu'à ce qu'un nouveau profil soit installé. C'est une volonté d'Apple, et il n'y a aucun moyen de contourner ce problème.

## Télécharger un profil
Téléchargez l'un des profils ici directement à l'aide de Safari sur votre appareil MacOS. Vous devez utiliser Safari pour télécharger le fichier.

!!! note
    Si vous ne savez pas quel fichier choisir, nous vous recommandons **DNS over HTTPS - 9.9.9.9 (DNSSEC, Blocage des menaces)**

* 9.9.9.9 (DNSSEC, Blocage des menaces)
    * [DNS over TLS - 9.9.9.9](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_20250129.mobileconfig) (Expire le 29 janvier 2025)
    * [DNS over HTTPS - 9.9.9.9](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_20250129.mobileconfig) (Expire le 29 janvier 2025)

* 9.9.9.10 (No DNSSEC, pas de blocage des menaces)
    * [DNS over TLS - 9.9.9.10](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_20250129.mobileconfig) (Expire le 29 janvier 2025)
    * [DNS over HTTPS  - 9.9.9.10](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_20250129.mobileconfig) (Expire le 29 janvier 2025)

* 9.9.9.11 (DNSSEC, Blocage des menaces, avec ECS)
    * [DNS over TLS - 9.9.9.11](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_ECS_20250129.mobileconfig) (Expire le 29 janvier 2025)
    * [DNS over HTTPS - 9.9.9.11](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_ECS_20250129.mobileconfig) (Expire le 29 janvier 2025)

* 9.9.9.12 (Pas de DNSSEC, pas de blocage des menaces, avec ECS)
    * [DNS over TLS - 9.9.9.12](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_ECS_20250129.mobileconfig) (Expire le 29 janvier 2025)
    * [DNS over HTTPS - 9.9.9.12](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_ECS_20250129.mobileconfig) (Expire le 29 janvier 2025)

## Installation

* Accédez à votre dossier Téléchargements et sélectionnez le profil que vous venez de télécharger.
    * Ouvrez `Règlages` > `Profile Téléchargé` et sélectionnez le profil Quad9 que vous avez ouvert.
        * Cliquez sur Installer
            * Entrez le PIN de votre téléphone

* Selectionnez Installer, puis Installer encore.

* Le profil est maintenant installé. Selectionnez `Terminer`

## Verifier la Configuration

Allez sur [on.quad9.net](https://on.quad9.net) depuis le navigateur de votre choix.

Des questions? Des Problèmes? Cela n'a pas fonctionné ? N'hesitez pas à nous contacter!

[Obtenir de l'aide](https://quad9.net/fr/support/contact){ .md-button .md-button--primary }
