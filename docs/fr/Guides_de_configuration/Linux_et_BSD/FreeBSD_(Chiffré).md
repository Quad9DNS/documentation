## Apperçu

Cet article décrit comment configurer et utiliser le service "local_unbound" préinstallé de FreeBSD afin d'envoyer du DNS chiffré via DNS over TLS à Quad9. 

Cela a été testé avec FreeBSD 13.1, mais devrait également fonctionner avec 12.X.

!!! warning "Firefox, VPNs"
    * **Firefox** est configuré pour utiliser Cloudflare DNS par défaut dans certaines régions. Si vous utilisez Firefox assurez vous que cette fonctionalité [soit desactivée](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **Les VPNs** ne respectent généralement pas les paramètres DNS du système ou du routeur. Si vous utilisez un VPN, configurez les adresses IP de Quad9 dans les paramètres « DNS personnalisé » de votre client VPN. Reportez-vous à la documentation de votre fournisseur VPN pour plus d'informations.

!!! warning
    FreeBSD installe, par défaut, une instance locale de Unbound DNS. Ceci est destiné à agir comme un redirecteur DNS local de mise en cache pour la machine locale uniquement, et n'est pas destiné à agir comme un redirecteur DNS pour d'autres périphériques réseau. Si vous souhaitez exécuter Unbound DNS sur FreeBSD dans le but d'exécuter un redirecteur DNS de mise en cache qui sera utilisé par plusieurs appareils sur le réseau, FreeBSD recommande d'installer le package dns/unbound à la place. Ces instructions ne sont valables que pour le service "local_unbound".

## Instructions

Vous aurez besoin de la commande sudo pour exécuter les commandes ci-dessous. Alternativement, vous pouvez simplement utiliser la commande su pour devenir l'utilisateur root et exécuter ces commandes directement en tant qu'utilisateur root, auquel cas vous devrez supprimer « sudo » de toutes les commandes ci-dessous.

* Installez la commande `dig` afin de pouvoir vérifier que la résolution DNS fonctionne comme prévu:

```
pkg install bind-tools
```

* Vérifiez que local_unbound est activé

```
sudo grep unbound /etc/rc.conf
```

Si le résultat suivant se produit, cela signifie que local_unbound est déjà activé et que vous pouvez ignorer l'instruction suivante et redémarrer le système:

```
local_unbound_enable="YES"
```

* S'il n'y a aucun résultat après cette commande, alors local_unbound doit être activé.
    * Dites au système que nous voulons utiliser local_unbound:
```
echo 'local_unbound_enable="YES"' >> /etc/rc.conf
```

Puis redémarrez le système (oui, vraiment):

```
reboot
```

* Activer local_unbound:

```
sudo local-unbound-setup
```

Le résultat devrait être similaire à celui-ci, mais peut différer légèrement:

```
destination: 
Extracting forwarders from /etc/resolv.conf.
/var/unbound/forward.conf not modified
/var/unbound/lan-zones.conf not modified
/var/unbound/control.conf not modified
/var/unbound/unbound.conf not modified
local_unbound not running? (check /var/run/local_unbound.pid).
Starting local_unbound.
/etc/resolvconf.conf created
Original /etc/resolv.conf saved as /var/backups/resolv.conf.20220625.200835
```

Cette commande sauvegardera les fichiers de configuration par défaut, téléchargera les fichiers de configuration modifiés à partir de la pièce jointe de cet article et redémarrera le service local_unbound.

```
sudo mv /var/unbound/forward.conf /var/unbound/forward-ORIG.conf && sudo mv /var/unbound/unbound.conf /var/unbound/unbound-ORIG.conf && sudo fetch -o /var/unbound/unbound.conf https://docs.quad9.net/assets/conf/freebsd/unbound.conf && sudo fetch -o /var/unbound/forward.conf https://docs.quad9.net/assets/conf/freebsd/forward.conf && sudo service local_unbound restart
```

These files are configured for our 9.9.9.9 service by default, without IPv6. If you'd like to use the .10 or .11 service instead, and/or enable IPv6, open the `/var/unbound/forward.conf` file and un-comment/comment out the appropriate lines. Ces fichiers sont configurés par défaut pour notre service 9.9.9.9, sans IPv6. Si vous souhaitez utiliser le service .10 ou .11 à la place et/ou activer IPv6, ouvrez le fichier `/var/unbound/forward.conf` et retirez/placez # sur les lignes appropriées.

## Verifier la Configuration

Dand l'éditeur de commande, exécutez la commande suivante:

```
dig +short txt proto.on.quad9.net.
```

Le résultat doit être `dot`, ce qui indique que les modifications ont réussi et que les requêtes sont chiffrées.

## Annuler

Pour annuler les modifications de configuration apportées à local_unbound, exécutez simplement cette commande pour restaurer les fichiers d'origine et redémarrez local_unbound :

```
sudo mv /var/unbound/forward-ORIG.conf /var/unbound/forward.conf && sudo mv /var/unbound/unbound-ORIG.conf /var/unbound/unbound.conf && sudo service local_unbound restart
```

Des questions? Des Problèmes? Cela n'a pas fonctionné? N'hesitez pas à nous contacter!

[Obtenir de l'aide](https://quad9.net/fr/support/contact){ .md-button .md-button--primary }
