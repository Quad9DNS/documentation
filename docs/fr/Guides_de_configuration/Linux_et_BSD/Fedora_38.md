## Apperçu

La manière la plus simple pour configurer Quad9 sur tout votre réseau se fait via les paramètres de votre routeur. Si vous préférez configurer Quad9 sur un appareil Windows individuel, veuillez suivre les étapes ci-dessous afin de configurer Fedora 38 pour utiliser Quad9.

!!! warning "Firefox, VPNs"
    * **Firefox** est configuré pour utiliser Cloudflare DNS par défaut dans certaines régions. Si vous utilisez Firefox assurez vous que cette fonctionalité [soit desactivée](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **Les VPNs** ne respectent généralement pas les paramètres DNS du système ou du routeur. Si vous utilisez un VPN, configurez les adresses IP de Quad9 dans les paramètres « DNS personnalisé » de votre client VPN. Reportez-vous à la documentation de votre fournisseur VPN pour plus d'informations.

## Instructions

### IPv4 

* Cliquez sur l'icône `Filaire` ou `WiFi` dans la barre d'outil en haut à droite de votre écran.
    * Cliquez sur l'icône `>` à côté de votre connection active.
        * Sélectionnez `Paramètre Filaire` ou `Paramètre Wifi`.

* Cliquez sur l'icône :gear: prêt de votre connection à droite .

* Cliquez sur l'onglet `IPv4`
	* Dans Methode IPv4 Sélectionnez `Manuel`
    * Dans `DNS` Désactivez `Automatique` 
        * Dans la barre écrivez `9.9.9.9, 149.112.112.112`


* Si vous n'utilisez pas IPv6, cliquez sur `Appliquer` pour compléter votre configuration puis confirmez que vous utilisez Quad9.


### IPv6 (Optionel)

Si votre réseau supporte IPv6, il est également recommandé de configurer l'addresse IPv6 de Quad9. Si vous n'êtes pas sûr que IPv6 soit configuré sur votre réseau, vous pouvez le vérifier ici: https://test-ipv6.com/

* Cliquez sur l'onglet `IPv4`
	* Dans Methode IPv4 Sélectionnez `Manuel`
    * Dans `DNS` Désactivez `Automatique` 
        * Dans la barre écrivez `2620:fe::fe, 2620:fe::9`




* Cliquez sur `Appliquer` pour compléter votre configuration

## Verifier la Configuration

Allez sur [on.quad9.net](https://on.quad9.net) depuis le navigateur de votre choix.

Des questions? Des Problèmes? Cela n'a pas fonctionné ? N'hesitez pas à nous contacter!

[Obtenir de l'aide](https://quad9.net/fr/support/contact){ .md-button .md-button--primary }
