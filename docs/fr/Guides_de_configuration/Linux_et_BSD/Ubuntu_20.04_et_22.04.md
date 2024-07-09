## Overview

Le moyen le plus simple de configurer Quad9 sur l'ensemble de votre réseau consiste à utiliser les paramètres de votre routeur. Si vous préférez configurer Quad9 sur un seul système, veuillez suivre les étapes ci-dessous pour configurer Ubuntu 22.04 ou 22.04 LTS pour utiliser Quad9.

!!! warning "Firefox, VPNs"
    * **Firefox** est configuré pour utiliser Cloudflare DNS par défaut dans certaines régions. Si vous utilisez Firefox assurez vous que cette fonctionalité [soit desactivée](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **Les VPNs** ne respectent généralement pas les paramètres DNS du système ou du routeur. Si vous utilisez un VPN, configurez les adresses IP de Quad9 dans les paramètres « DNS personnalisé » de votre client VPN. Reportez-vous à la documentation de votre fournisseur VPN pour plus d'informations.

## Instructions

### IPv4 

* Depuis le bureau Ubuntu, sélectionnez le menu déroulant dans le coin supérieur droit de l'écran, développez `Wired Connection` ou `Wireless Connection` en fonction de votre type de connexion, puis sélectionnez `Wired Settings` ou `Wireless Settings`.

* Cliquez sur l'icône :gear: icon à côté de votre connexion.

* Cliquez sur `IPv4` tab
    * Désactivez `Automatic DNS`
        * Entrez les adresses IP Quad9 de vos services préférés.

Plusieurs adresses IP peuvent être saisies dans la liste à l'aide de virgules.

`9.9.9.9, 149.112.112.112`

* Si vous ne souhaitez pas utiliser IPv6, cliquez sur `Appliquer` afin de terminer le processus de configuration, puis confirmez que vous utilisez Quad9.


### IPv6 (Optionel)

Si votre réseau/ordinateur prend en charge IPv6, il est également recommandé de configurer les adresses IPv6 de Quad9. Si vous n'êtes pas sûr qu'IPv6 soit configuré sur votre réseau, vous pouvez le tester ici : https://test-ipv6.com/


* Selectionnez `IPv6` tab
    * Désactivez `Automatic DNS`
        * Entrez les adresses IP Quad9 de vos services préférés.

Plusieurs adresses IP peuvent être saisies dans la liste à l'aide de virgules.

`2620:fe::fe, 2620:fe::9`

* Click `Apply` to complete the setup process.

## Verifier la Configuration

Allez sur [on.quad9.net](https://on.quad9.net) depuis le navigateur de votre choix.

Des questions? Des Problèmes? Cela n'a pas fonctionné? N'hesitez pas à nous contacter!

[Obtenir de l'aide](https://quad9.net/fr/support/contact){ .md-button .md-button--primary }
