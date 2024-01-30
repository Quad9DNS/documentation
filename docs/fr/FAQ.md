## Comment puis-je confirmer que j'utilise Quad9?

Le test le plus simple consiste à ouvrir [on.quad9.net](https://on.quad9.net) dans le navigateur de votre choix.

## Test de protocole - Confirmez sur quel protocole Quad9 a reçu votre requête

Ceci est particulièrement pertinent après la configuration du chiffrage DNS, tel que DNS over TLS ou DNS over HTTPS, dans le système d'exploitation, le routeur, le DNS forwarder.

Exécutez la commande suivante et reportez-vous aux réponses possibles ci-dessous :

=== "Windows (PowerShell/Terminal)"

    `Resolve-DnsName -Type txt proto.on.quad9.net.`
=== "MacOS/Linux/Unix (Terminal)"

    `dig +short txt proto.on.quad9.net.`

Réponses possibles:

* do53-udp (53/UDP - Plaintext)
* do53-tcp (53/TCP - Plaintext)
* doh (443/TCP - DNS over HTTPS)
* dot (853/TCP - DNS over TLS)
* dnscrypt-udp (UDP - DNSCrypt)
* dnscrypt-tcp (TCP - DNSCrypt)

Si vous ne recevez pas de réponse (NXDOMAIN), cela signifie que Quad9 n'a pas été utilisé pour effectuer cette requête DNS.

## Identifier un blocage Quad9

Le moyen le plus rapide de voir si un domaine est bloqué par Quad9 consiste à utiliser notre [Blocked Domain Tester](https://quad9.net/result).

Quand Quad9 bloque un domaine, la réponse est `NXDOMAIN`. `NXDOMAIN` est également renvoyé lorsqu'un domaine n'existe pas. Pour différencier les domaines inexistants et les domaines bloqués, nous configurons la valeur `AUTHORITY` différemment. Si vous recevez `NXDOMAIN` avec `AUTHORITY: 0`, c'est un blocage de la part de Quad9. Si vous recevez `NXDOMAIN` *avec* `AUTHORITY: 1`, cela signifie que c'est un domaine qui n'existe pas.

Un domaine échouera egalement à se résoudre si l'authentification DNSSEC échoue, le résultat donnera le code `SERVFAIL` au lieu de `NXDOMAIN`.

=== "Domaine bloqué"

    `dig @9.9.9.9 isitblocked.org | grep "status\|AUTHORITY"`
    ```
    ;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 29193
    ;; flags: qr rd ad; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1
    ```
=== "Domaine inexistant"

    `dig @9.9.9.9 sfaisofnadgre.odafds | grep "status\|AUTHORITY:"`
    ```
    ;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 22595
    ;; flags: qr rd ra ad; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1
    ```
=== "Erreur DNSSEC"
    
    `dig @9.9.9.9 A brokendnssec.net +dnssec | grep status`
    ```
    ;; ->>HEADER<<- opcode: QUERY, status: SERVFAIL, id: 40999
    ```

## Détecter la redirection transparente DNS (Hijacks)

Certains FAI, le plus souvent en Asie, en Afrique ou au Moyen-Orient, redirigeront de manière transparente les requêtes DNS destinées aux services DNS tiers, comme Quad9, vers leurs propres DNS forwarders/serveurs. Il peut s'agir d'une tentative d'appliquer des politiques/lois locales, ou simplement d'augmenter le taux de HIT du cache sur leurs DNS forwarders.

Vous pouvez détecter une redirection DNS transparente en exécutant la commande suivante à partir de l'invite de commande ou du terminal de n'importe quel système d'exploitation. Si la réponse est autre chose que `resXXX.xxx.rrdns.pch.net`, alors le DNS est redirigé de manière transparente.

=== "Windows (PowerShell)"

    ```
    nslookup -q=txt -class=chaos id.server. 9.9.9.9 | Select-String "pch"
    ```

=== "MacOS/Linux/BSD (Terminal)"
    ```
    dig +short ch txt id.server. @9.9.9.9
    ```
Si le résultat ne ressemble pas à ce qui suit ou s’il n’y a aucun résultat, le DNS est redirigé de manière transparente.

=== "Windows (PowerShell)"
    ```
    Non-authoritative answer:
    "res200.vie.rrdns.pch.net"
    ```

=== "MacOS/Linux/BSD (Terminal)"
    ```
    "res860.qfra3.rrdns.pch.net"
    ```
### Mon FAI redirige le DNS de manière transparente. Maintenant quoi?

Veuillez vous référer à nos guides de configuration annexés à `(Encrypted)` dans le titre. En utilisant le DNS chiffré, la redirection transparente du DNS ne sera pas possible.

## Qu'est ce que EDNS Client Subnet (ECS)?

Le service Quad9 `9.9.9.11` utilise ECS.

EDNS Client Subnet (ECS) permet à Quad9 d'envoyer une partie de votre adresse IP à des serveurs de noms faisant autorité, ce qui aide les principaux fournisseurs de contenu (CDN), tels que Google, Microsoft, etc., à déterminer avec précision votre géolocalisation.

ECS n'aura aucun effet sur l'emplacement Quad9 auquel vos requêtes sont envoyées, il affecte simplement les informations que Quad9 transmet au nom de serveur faisant autorité et peut affecter l'adresse IP qu'elles renvoient. Quad9 utilise l'adressage anycast pour garantir que vous êtes acheminé vers l'emplacement Quad9 le plus proche disponible, que vous utilisiez ou non notre service ECS.

Étant donné qu'ECS ne joue aucun rôle dans la détermination de la destination d'envoi de vos requêtes, il n'a aucun effet positif ou négatif sur le temps d'aller-retour (ping) vers Quad9.

ECS peut être considéré comme un compromis entre la confidentialité et l’obtention de contenu géospécifique. Une option pour l'utilisateur soucieux de la confidentialité consiste à le laisser désactivé et à l'activer uniquement si vous remarquez qu'un domaine spécifique ne vous fournit pas le contenu correct ou ne se charge pas du tout.

## Fournisseurs réseau / Tests de leak DNS

Quad9 utilizes multiple network providers in our global network. When running a DNS leak test, it's expected to see IP addresses owned by the following providers:Quad9 utilise plusieurs fournisseurs de réseau dans notre réseau mondial. Lors de l'exécution d'un test de leak DNS, il est configuré pour voir les adresses IP appartenant aux fournisseurs suivants :

!!! note "Outils recommandé pour les tests de leak DNS"
    [dnscheck.tools](https://dnscheck.tools/)

* WoodyNet (AKA PCH.net)
* PCH.net
* GSL Networks
* i3D
* EdgeUno
* Equinix Metal (FKA: Packet, Packet.net, or Packethost)
* Path.net (Path Network)

Ces organisations sont également répertoriées sur la page Sponsors du site Quad9 : [quad9.net/about/sponsors](https://quad9.net/fr/about/sponsors)

Si vous essayez simplement de déterminer si vous utilisez Quad9, vous pouvez visiter [on.quad9.net](https://on.quad9.net) au lieu de vous reporter à un test de leak DNS. Cependant, un test de leak DNS peut être utile pour garantir que vous utilisez exclusivement Quad9, ce qui est nécessaire pour garantir que toutes vos requêtes DNS seront protégées par Quad9.
