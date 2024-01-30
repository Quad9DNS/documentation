## Aperçu

pfSense est un routeur et pare-feu open-source, utilisé dans les structures grand public et commerciales.

pfSense a une [documentation pour DNS over TLS](https://docs.netgate.com/pfsense/en/latest/recipes/dns-over-tls.html), que nous vous recommandons de consulter en plus de cet article.

OPNsense utilises Unbound, qui est compatible avec DNS over TLS, la configuration est accessible dans le GUI.

!!! warning "C'est l'heure du Backup!"
    Avant d'apporter des modifications à un environnement de production, nous vous recommandons de [sauvegarder la configuration existante](https://docs.netgate.com/pfsense/en/latest/backup/configuration.html)

## Instructions

Allez dans `System` -> `Generate Setup` dans le menu en haut.

* Cliquez sur `Add DNS Server` jusqu'à ce qu'il y ait 4 lignes d'entrées disponibles.
* Add Ajoutez les adresses IPv4 et IPv6 de Quad9 dans les champs de gauche:
`9.9.9.9`,`149.112.112.112`,`2620:fe::fe`,`2620:fe::9`

!!! warning "IPv6"
    Si votre réseau ne dispose pas d'IPv6, ce que vous pouvez vérifier ici, alors les adresses IPv6 ne doivent pas être ajoutées, car cela pourrait entraîner l'échec d'un nombre conséquent de vos requêtes DNS.

* Ajoutez `dns.quad9.net` dans tous les champs Hostname à droite.

Cliquez sur "Enregistrer" en bas de l'écran.

Allez dans `Services` -> `DNS Forwarder` dans le menu en haut.
* Assurez vous que `Enable DNS forwarder` soit désactivé. Si cette option est activée, désactivez la, et cliquez `Save` en bas de la page.

Allez dans `Services` -> `DNS Resolver` dans le menu du haut.

* Désactivez `Enable DNSSEC Support`
* Activez `DNS Query Forwarding`
* Activez `Use SSL/TLS for outgoing DNS queries to Forwarding Servers`
* Cliquez sur `Save` en bas de l'écran.
* Cliquez sur `Apply Changes` prêt du haut de l'écran pour appliquer et sauvegarder les changements.

## Verifier la Configuration

Vous pouvez confirmer que pfSense envoie désormais vos requêtes via DNS over TLS à l'aide de l'outil Packet Capture intégré.

Vous pouvez également tester à partir d'un système macOS, Linux ou Windows connecté à ce routeur/pare-feu pfSense.

Vous avez des questions? Vous rencontrez un probleme? Cela n'a pas marché? N'hésitez pas à nous contacter!

[Obtenir de l'aide](https://quad9.net/fr/support/contact){ .md-button .md-button--primary }
