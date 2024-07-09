## Apperçu

Cet article décrit comment configurer et utiliser Unbound sur OpenBSD afin d'envoyer un DNS crypté via DNS over TLS to Quad9.

Cela a été testé avec OpenBSD 7.1.

!!! warning "Firefox, VPNs"
    * **Firefox** est configuré pour utiliser Cloudflare DNS par défaut dans certaines régions. Si vous utilisez Firefox assurez vous que cette fonctionalité [soit desactivée](https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
    * **Les VPNs** ne respectent généralement pas les paramètres DNS du système ou du routeur. Si vous utilisez un VPN, configurez les adresses IP de Quad9 dans les paramètres « DNS personnalisé » de votre client VPN. Reportez-vous à la documentation de votre fournisseur VPN pour plus d'informations.

!!! warning
    Unbound DNS est installé par défaut sur les installations OpenBSD standard. Le but est d'agir comme un redirecteur DNS local de mise en cache pour la machine locale uniquement, et non pas à agir comme un redirecteur DNS pour d'autres périphériques réseau. Si vous souhaitez exécuter Unbound DNS sur OpenBSD dans le but d'exécuter un redirecteur DNS de mise en cache qui sera utilisé par plusieurs périphériques sur le réseau, vous pouvez modifier de manière appropriée les valeurs d'interface et de contrôle d'accès dans unbound.conf, qui par défaut, autorise uniquement les requêtes DNS de localhost.

## Instructions

Vous devez être connecté en tant qu'utilisateur root directement ou en exécutant la commande `su` et en saisissant votre mot de passe dans une session Terminal.

* Installez wget s'il n'est pas déjà installé.
```
pkg_add wget
```

* Sauvegardez un backup du fichier unbound.conf original et téléchargez le fichier de remplacement « unbound.conf », préconfiguré pour envoyer des requêtes DNS à Quad9 via DNS over TLS.

!!! note
    Nous vous encourageons à télécharger et inspecter le fichier unbound.conf dans un éditeur de texte, joint à cet article, avant de le télécharger sur votre système OpenBSD.

```
mv /var/unbound/etc/unbound.conf /var/unbound/etc/unbound.BAK && wget -O /var/unbound/etc/unbound.conf https://docs.quad9.net/assets/conf/openbsd/unbound.conf
```

Optionel: Si votre réseau prend en charge IPv6, ouvrez le fichier, /var/unbound/etc/unbound.conf sur OpenBSD avec l'éditeur de texte de votre choix, et apportez les modifications suivantes, en supprimant le # (commentaire) avant le début de ces lignes.

**Avant**

```
# do-ip6: no
# forward-addr: 2620:fe::fe@853#dns.quad9.net
# forward-addr: 2620:fe::9@853#dns.quad9.net
```

**Après**

```
do-ip6: yes
forward-addr: 2620:fe::fe@853#dns.quad9.net
forward-addr: 2620:fe::9@853#dns.quad9.net
```

* Définissez Unbound pour qu'il démarre au démarrage du système et activez le service (exécutez ces commandes une par une) :

```
rcctl enable unbound
```
```
rcctl start unbound
```

## Verifier la Configuration

* Assurez-vous qu'Unbound peut répondre aux requêtes DNS:

```
dig +short quad9.net @127.0.0.1
```
* Le résultat de cette requête devrait être `dot.`, ce qui indique que Quad9 reçoit la requête DNS via DNS over TLS.

```
dig +short txt proto.on.quad9.net.
```

Configurez votre système pour qu'il commence à utiliser Unbound pour DNS en sauvegardant le fichier resolv.conf existant et en définissant 127.0.0.1 comme serveur DNS pour le système.:
```
cp /etc/resolv.conf /etc/resolv.BAK && echo "nameserver 127.0.0.1" > /etc/resolv.conf
```

## Annuler

Si vous souhaitez arrêter d'utiliser Unbound comme serveur DNS, restaurez simplement le fichier backup resolv.conf que vous aviez sauvegardé:

```
mv /etc/resolv.BAK /etc/resolv.conf
```

Des questions? Des Problèmes? Cela n'a pas fonctionné? N'hesitez pas à nous contacter!

[Obtenir de l'aide](https://quad9.net/fr/support/contact){ .md-button .md-button--primary }
