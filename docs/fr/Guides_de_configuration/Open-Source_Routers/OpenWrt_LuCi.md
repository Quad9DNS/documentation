## Aperçu

Le projet OpenWrt est un système d'exploitation Linux ciblant les appareils embarqués, souvent utilisé comme solution open source pour les routeurs et les pare-feu.

Ce guide couvre la configuration de Quad9 dans les paramètres du redirecteur DNS. Lorsque vous utilisez votre routeur OpenWrt comme serveur DNS, il transmettra les requêtes DNS à Quad9.

!!! warning "C'est l'heure du Backup!"
    Avant d'apporter des modifications à un environnement de production, nous vous recommandons de [sauvegarder la configuration existante](https://openwrt.org/docs/guide-user/troubleshooting/backup_restore)

## Instructions

* Connectez-vous à votre panneau de configuration LuCI, généralement en ouvrant `http://192.168.1.1` dans votre navigateur.

* Allez dans `Network` -> `DHCP and DNS`
    * Entrez `9.9.9.9` et `149.112.112.112`, ou les adresses de votre service Quad9 préféré dans les champs de saisie « Redirections DNS ».

* Si votre réseau supporte IPv6, vous pouvez aussi ajouter 2620:fe::fe et 2620:fe::9, ou l'adresse IPv6 de votre service Quad9 préféré.

* Allez dans l'onglet `Resolv and Hosts Files`, et assurez vous que `Ignore resolv file` soit `Enabled`.

* Cliquez sur `Save & Apply` en bas. Puisque vous ne modifiez pas les paramètres DHCP, le changement devrait être instantané.

## Verifier la Configuration

* Confirmez que vous utilisez Quad9 sous Linux, MacOS ou Windows.

Vous avez des questions? Vous rencontrez un probleme? Cela n'a pas marché? N'hésitez pas à nous contacter!

[Obtenir de l'aide](https://quad9.net/fr/support/contact){ .md-button .md-button--primary }
