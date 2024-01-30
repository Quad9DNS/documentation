## Aperçu

OPNsense est un routeur et pare-feu open-source firewall and router, utilisé dans les structures grand public et commerciales.

OPNsense utilises Unbound, qui est compatible avec DNS over TLS, la configuration est accessible dans le GUI.

!!! warning "C'est l'heure du Backup!"
    Avant d'apporter des modifications à un environnement de production, nous vous recommandons de [sauvegarder la configuration existante](https://docs.opnsense.org/manual/backups.html#backup)

### Instructions

* Allez dans `Services` -> `DNS over TLS` dans le menu de gauche
    * Cliquez sur le boutton +
        * Ajoutez 4 entrées, en utilisant `dns.quad9.net` dans le champ **Verify CN**, et `853` dans le champ **Server Port:**.

Server IP: `9.9.9.9`
Server IP: `149.112.112.112`
Server IP: `2620:fe::fe`
Server IP: `2620:fe::9`

!!! warning "IPv6"
    Si votre réseau ne dispose pas d'IPv6, ce que vous pouvez vérifier ici, alors les adresses IPv6 ne doivent pas être ajoutées, car cela pourrait entraîner l'échec d'un nombre conséquent de vos requêtes DNS.

* Cliquez sur `Apply` pour enregistrer les modifications.

* Allez dans `System` -> `Settings` -> `General` dans le menu de gauche.

* Désactivez `Allow DNS server list to be overridden by DHCP/PPP on WAN`
* Cliquez sur `Save`
* Cliquez sur `Apply` en haut de la page.

## Verifier la Configuration

Afin de confirmer qu'OPNsense envoie désormais vos requêtes via DNS over TLS, vous pouvez exécuter un packet capture dans la ligne de commande:

```
tcpdump -i em0 'port 853'
```

!!! note
    Vous devrez peut-être ajuster le nom de l'interface em0 à celui de l'interface WAN de votre appareil.

Vous pouvez également tester à partir d'un système macOS, Linux ou Windows connecté à ce routeur/pare-feu OPNsense.

Vous avez des questions? Vous rencontrez un probleme? Cela n'a pas marché? N'hésitez pas à nous contacter!

[Obtenir de l'aide](https://quad9.net/fr/support/contact){ .md-button .md-button--primary }
