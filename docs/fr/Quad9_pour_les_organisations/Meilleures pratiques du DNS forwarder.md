## Aperçu

Vous administrez le DNS d'un immeuble, d'un bureau, d'une entreprise, d'un fournisseur d'acces internet, etc. et vous souhaitez utiliser Quad 9. Excellent choix !
!!! note

    Pour les FAI ou les organisations comptant plus de 5 000 utilisateurs derrière les forwarders DNS, ou si vous attendez plus de 500 requêtes par seconde à partir d'une seule adresse IP de sortie, veuillez contacter [Quad9 Support](https://quad9.net/support/contact) avec les détails de votre configuration, afin que nous puissions garantir un déploiement fluide et réussi.

Les transitaires de mise en cache et leur configuration optimale sont essentielles lors de l'envoi massif de requêtes à Quad9, et sont fortement préférées à l'affectation directe via DHCP aux utilisateurs finaux en ce qui concerne:

### Performance
Réduire le nombre de requêtes récurrentes sur Quad9, économiser de la bande passante et offrir une expérience plus rapide à l'utilisateur final lorsque ses requêtes sont déjà dans le cache des forwarders.


### Sécurité
L'activation de la journalisation des requêtes ou de certains types de métriques de haut niveau est conseillée pour identifier une éventuelle compromission provenant de points finaux ou de clients spécifiques, elle est parfois requise par la législation locale.

### Politique locale
La possibilité de bloquer ou d'analyser certains FQDN au niveau du forwarder donne plus de contrôle à l'administrateur réseau sans compter exclusivement sur Quad9 pour bloquer les domaines malveillants.

Lorsque vous configurez Quad9 comme résolveur récursif dans votre infrastructure et que vous mettez en cache les forwarders DNS, veuillez prendre en compte les bonnes pratiques suivantes.

### Exclusivité

Étant donné que les forwarders DNS utilisent un ordre circulaire lors du transfert de requêtes vers une liste de serveurs DNS récursifs, Quad9 doit être défini comme serveur DNS récursif exclusif dans vos forwarders. L'ajout de serveurs DNS récursifs supplémentaires en dehors de Quad9  entraînera un pourcentage de vos requêtes DNS non protégées par le blocage des menaces de Quad9.

### Mise en cache

Il est impératif que vos forwarders DNS soient configurés pour mettre en cache les données de réponse afin d'éviter les requêtes récursives excessives vers Quad9 et de fournir une résolution DNS beaucoup plus rapide pour les appareils du réseau.

Assurez-vous que vos forwarders DNS disposent de suffisamment de mémoire ou d'espace disque alloué au cache pour éviter qu'il ne sature.

La quantité de mémoire qui doit être dédiée à la mise en cache DNS varie considérablement entre megabits et gigabits en fonction de la quantité de requêtes DNS provenant des points de terminaison de votre réseau.

=== "BIND"
    Lie les caches en mémoire par défaut, la seule limitation est donc l'épuisement de la mémoire disponible dans le système.

    Pour vérifier la taille du cache actuel, vous pouvez vider le cache dans un fichier local, puis examiner la taille du fichier, qui correspondra approximativement à la quantité de mémoire utilisée par le cache :

    ```
    rndc dumpdb -all
    ```

    ```
    ls -alh /var/bind/
    ```
=== "dnsdist"
    La mise en cache est désactivée par défaut, mais [peut être activée pour le stockage mémoiree](https://dnsdist.org/guides/cache.html).
=== "Unbound"
    La taille du cache allouée est déterminée par les options msg-cache-size et rrset-cache-size dans le fichier [unbound.conf file](https://www.nlnetlabs.nl/documentation/unbound/unbound.conf/).

    Vous pouvez vérifier la quantité de mémoire que votre cache utilise actuellement pour la comparer à la taille du cache que vous avez allouée dans unbound.conf en utilisant la [commande unbound-control](https://www.nlnetlabs.nl/documentation/unbound/unbound-control/) pour afficher les statistiques des valeurs mem.cache.rrset et mem.cache.message.

=== "Knot Resolver"
    Knot Resolver met en cache sur le disque par défaut, mais peut être configuré pour utiliser la mémoire/tmpfs, les backends et partager le cache entre les instances. Knot Resolver a [une excellente documentation sur tout ce qui concerne la mise en cache](https://knot-resolver.readthedocs.io/en/stable/daemon-bindings-cache.html).
=== "Windows DNS Server"

    La mise en cache en mémoire peut être configurée en utilisant la commande `Set-DnsServerCache`.

    L'utilisation de la mémoire peut être vérifiée à l'aide de la commande `Get-DnsServerStatistics`.

### Utiliser les adresses IP Quad9 primaire et secondaire

La configuration de l'adresse IP principale *et* secondaire de votre service Quad9 souhaité permet d'équilibrer naturellement la charge des requêtes DNS dans l'infrastructure Quad9.

### Utiliser IPv6

Si votre réseau est compatible IPv6, configurez également les adresses IPv6 principale et secondaire du service Quad9 souhaité dans vos forwarders DNS, ce qui permet d'équilibrer naturellement la charge des requêtes DNS dans l'infrastructure Quad9.

Si IPv6 n'est pas utilisé, Quad9 vous encourage fortement à rechercher comment l'activer sur votre réseau. Les chemins de routage IPv6 sont souvent plus rapides que les chemins IPv4, ce qui augmente les chances de succès, à des vitesses plus rapides et avec une meilleure redondance.

### Adresses IP distinctes pour chaque forwarder DNS

Idéalement, chaque forwarder DNS devrait envoyer et recevoir des requêtes DNS à Quad9 en utilisant différentes adresses publiques IPv4 et IPv6, même si les adresses se trouvent sur le même subnet.

### Désactiver la validation DNSSEC

Étant donné que Quad9 effectue déjà la validation DNSSEC, l'activation de DNSSEC dans le forwarder entraînera une duplication du processus DNSSEC, réduisant considérablement les performances et provoquant potentiellement de fausses réponses BOGUS.

=== "dnsdist"
    Ajoutez ceci dans `dnsdist.conf` *au dessus* de votre pool d'affectation.
    ```
    if noDNSSECOnNOSEC then
      addAction(NetmaskGroupRule(nmgNOSEC, false), SetDisableValidationAction(), { name="R_NO_DS" })
    end
    ```
=== "Knot Resolver"
    Ajoutez ceci dans le fichier `kresd.conf` et rechargez/redémarrez le service `kresd` .
    ```
    -- turns off DNSSEC validation
    trust_anchors.remove('.')
    ```
=== "PowerDNS Recursor"
    Dans `recursor.conf`, désactivez `dnssec` et rechargez/redémarrez `pdns-recursor`.
    ```
    dnssec=off
    ```
=== "Unbound"
    Retirez ces lignes dans `unbound.conf` et rechargez/redémarrez unbound.
    ```
    trust-anchor-file:
    auto-trust-anchor-file:
    trust-anchor:
    trusted-keys-file:
    ```

### Désactiver QNAME Minimization

QNAME Minimization est une fonctionnalité de confidentialité destinée à être utilisée lorsque vous utilisez un résolveur récursif (Quad9), mais dans un forwarder DNS, elle n'apporte aucune amélioration de la confidentialité et réduit considérablement les performances. [Qu'est ce que QNAME Minimization?](https://www.isc.org/blogs/qname-minimization-and-privacy/)

=== "BIND"
    Dans ```options {``` section du fichier named.conf, ajoutez la ligne suivante et rechargez/redémarrez named/bind9.
    ```
    qname-minimization disabled;
    ```
=== "dnsdist"
    QNAME Minimization n'est pas supporté dans dnsdist. Rien à faire ici.
=== "Unbound"
    ajoutez la ligne suivante dans `unbound.conf` et rechargez/redémarrez unbound. 
    ```
    qname-minimisation: no
    ```
=== "Knot Resolver"
    Dans le fichier `kresd.conf`, ajouter cette ligne pour désactiver QNAME Minimization et rechargez/redémarrez le service `kresd` .
    ```
    policy.add(policy.all(policy.FLAGS('NO_MINIMIZE')))
    ```

Des questions? Des problèmes? N'hésitez pas à nous contacter!

[Obtenir de l'aide](https://quad9.net/fr/support/contact){ .md-button .md-button--primary }
