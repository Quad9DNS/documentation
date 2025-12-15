## Aperçu

Ubuntu 22.04 et Linux Mint 20.3 ou ses versions plus récentes incluent DNS over TLS en systemd-resolved, mais l'option n'est pas disponible dans le GUI.

!!! bug
    Techniquement, bien qu'elle soit également compatible avec Ubuntu *20.04*, nous ne recommandons pas l'utilisation de cette méthode sur la version 20.04 car la version de son systemd-resolv est plus ancienne, ce qui peut occasioner des problèmes.

!!! bug
    L'option DNSSEC ne doit pas être activée dans systemd-resolved. Elle est extrêmement bugée et ne ferait que dupliquer le processus de validation DNSSEC déjà effectué par Quad9, ce qui réduirait considérablement les performances.

!!! warning "Firefox, VPNs"
    * **Firefox** est configuré pour utiliser Cloudflare DNS par défaut dans certaines régions. Si vous utilisez Firefox assurez vous que cette fonctionalité soit desactivée.
    * **Les VPNs** ne respectent généralement pas les paramètres DNS du système ou du routeur. Si vous utilisez un VPN, configurez les adresses IP de Quad9 dans les paramètres « DNS personnalisé » de votre client VPN. Reportez-vous à la documentation de votre fournisseur VPN pour plus d'informations.

## Instructions

* Configurer Quad9 dans les paramètres réseau ([Ubuntu](editme), [Linux Mint](editme)).

* Ouvrez l'application `Terminal`, et copiez/collez ces lignes de commande afin d'activer DNS over TLS.Lorsque vous êtes invité à saisir votre mot de passe, saisissez-le et appuyez sur `Entrée`.

```
sudo sed -i 's/#DNSOverTLS=no/DNSOverTLS=yes/g' /etc/systemd/resolved.conf
```

* Redémarer `systemd-resolvd` et `networking services` afin d'enregistrer les changements dans le fichier:

```
sudo systemctl restart systemd-resolved.service && sudo service network-manager restart
```
## Verifier la Configuration

* Verifiez que DNS over TLS est actif en ouvrant l'application `Terminal` et entrez les commandes suivantes, saisissez votre mot de passe et appuyez sur `Entrée`:

```
dig +short txt proto.on.quad9.net.
```
Si la réponse est `dot.`, cela signifie que ca marche! Si la réponse est `do53-udp.`, alors il utilise encore du plaintext. S'il n'y a pas de réponse, cela signifie que Quad9 n'a probablement pas été configuré dans le `Paramètres réseau`.

## Annuler

Si vous rencontrez des problèmes ou souhaitez annuler ce changement de configuration :

* Ouvrez l'application `Terminal`, et copiez/collez ces lignes de commande afin de désactiver DNS over TLS. Lorsque vous êtes invité à saisir votre mot de passe, saisissez-le et appuyez sur `Entrée`.

```
sudo sed -i 's/DNSOverTLS=yes/#DNSOverTLS=no/g' /etc/systemd/resolved.conf
```

* Redémarrez les services `systemd-resolvd` et `networking` afin d'enregistrer les changements que nous venons d'effectuer dans le fichier:

```
sudo systemctl restart systemd-resolved.service && sudo service network-manager restart
```

Vous avez des questions? Vous rencontrez un probleme? Cela n'a pas marché? N'hésitez pas à nous contacter!

[Obtenir de l'aide](https://quad9.net/fr/support/contact){ .md-button .md-button--primary }
