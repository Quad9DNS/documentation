## Apperçu

La manière la plus simple pour configurer Quad9 sur tout votre réseau se fait via les paramètres de votre routeur. Si vous préférez configurer Quad9 sur un appareil Windows individuel, veuillez suivre les étapes ci-dessous afin de configurer Windows 11 pour utiliser Quad9.

!!! warning "Firefox, VPNs"
    * **Firefox** est configuré pour utiliser Cloudflare DNS par défaut dans certaines régions. Si vous utilisez Firefox assurez vous que cette fonctionalité [soit desactivée](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **Les VPNs** ne respectent généralement pas les paramètres DNS du système ou du routeur. Si vous utilisez un VPN, configurez les adresses IP de Quad9 dans les paramètres « DNS personnalisé » de votre client VPN. Reportez-vous à la documentation de votre fournisseur VPN pour plus d'informations.
    

## Instructions

### IPv4

* Faites un clic droit sur votre icône réseau (Filaire ou WiFi) dans la barre d'outil en bas à droite et cliquez sur `Ouvrir les paramètres réseau et Internet`.

* Sélectionnez `Propriétés`.

* Sur `Attribution du serveur DNS` Cliquez sur `Modifier`.

* Faites les changements suivants :

	* Changez l'option `Automatique (DHCP)` sur `Manuel`
	* Cliquez sur l'icône sous `IPv4` pour l'activer. Assurez vous que IPv4 soit activé en bleu.
	* Entrez: `9.9.9.9` dans la barre `DNS preféré`.
		* Dans `Chiffrement DNS préféré` sélectionnez `Chiffré uniquement (DNS over HTTPS)`
	* Entrez: `149.112.112.112` dans la barre `Autre DNS`. 
		*Dans `Chiffrement DNS auxiliaire` sélectionnez `Chiffré uniquement (DNS over HTTPS)

* Cliquez sur `Enregistrer`


### IPv6

Si votre réseau supporte IPv6, il est également recommandé de configurer l'addresse IPv6 de Quad9. Si vous n'êtes pas sûr que IPv6 soit configuré sur votre réseau, vous pouvez le vérifier ici: https://test-ipv6.com/

* Suivez le même procédé que pour IPv4. Cliquez sur l'icône sous `IPv6`. Assurez vous que IPv6 soit activé en bleu.

* Entrez: `2620:fe::fe` dans la barre sous `DNS preféré`.
	* Dans `Chiffrement DNS préféré` sélectionnez `Chiffré uniquement (DNS over HTTPS)`

* Entrez: `2620:fe::9` dans la barre sous `Autre DNS`.
	*Dans `Chiffrement DNS auxiliaire` sélectionnez `Chiffré uniquement (DNS over HTTPS)

* Cliquez sur `Enregistrer`.

* Fermez toutes les fenêtres de configuration Windows.


## Verifier la Configuration


* Ouvrez le Terminal Windows Powershell et exécutez cette commande:

```
Resolve-DnsName -Type txt proto.on.quad9.net.
```

Le résultat devrait montrer `doh.` (DNS over HTTPS) dans la section `NameHost` si vous définissez Quad9 dans les paramètres réseau et activez le chiffrement.

```
Name                           Type   TTL   Section    NameHost
----                           ----   ---   -------    --------
proto.on.quad9.net             CNAME  60    Answer     doh
```

Des questions? Des Problèmes? Cela n'a pas fonctionné? N'hesitez pas à nous contacter!

[Obtenir de l'aide](https://quad9.net/fr/support/contact){ .md-button .md-button--primary }
