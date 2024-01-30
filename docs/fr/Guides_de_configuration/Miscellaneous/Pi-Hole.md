## Aperçu

Pi-Hole est un redirecteur DNS populaire, souvent utilisé principalement pour bloquer les domaines spécifiquement associés aux publicités et aux trackers.

## Pi-Hole Configuration

Pour des instructions de configuration détaillées de Pi-Hole lui-même, veuillez consulter la [Documentation officielle de Pi-Hole](https://docs.pi-hole.net/).

## Instructions

Une fois que vous avez installé Pi-Hole et que vous pouvez accéder au panneau d'administration, Quad9 est déjà l'une des options par défaut.

* Dans le panneau d'administration, allez dans `Settings` -> `DNS`
    * Cochez les deux cases IPv4 à côté de Quad9 (filtered, DNSSEC)
        * Si votre réseau ne dispose pas d'IPv6, ce que vous pouvez vérifier ici, alors les adresses IPv6 ne doivent pas être ajoutées, car cela pourrait entraîner l'échec d'un nombre conséquent de vos requêtes DNS. [Test here](https://port.tools/ipv6-test/).

* Activez les options:
    * `Never forward non-FQDNs`
    * `Never forward reverse lookups for private IP ranges`
        * Click `Save` at the bottom.

## Verifier la Configuration

Une fois Quad9 configuré dans Pi-Hole, vous pouvez configurer votre routeur ou un seul ordinateur pour utiliser l'adresse IP du Pi-Hole comme serveur DNS. Si le journal des requêtes est activé (Paramètres -> Confidentialité [tab]), vous devriez voir Quad9 enregistré dans la colonne Statut.

## Domaines Bloqués

Les domaines bloqués par Quad9 seront enregistrés comme Bloqués (externe, NXRA) dans la colonne Statut du journal des requêtes.

Vous avez des questions? Vous rencontrez un probleme? Cela n'a pas marché? N'hésitez pas à nous contacter!

[Obtenir de l'aide](https://quad9.net/fr/support/contact){ .md-button .md-button--primary }
