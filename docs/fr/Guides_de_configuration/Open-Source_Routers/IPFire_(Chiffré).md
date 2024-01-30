## Aperçu

IPFire est un routeur et pare-feu open-source, utilisé dans les structures grand public et commerciales.

IPFire utilises Unbound, qui est compatible avec DNS over TLS, la configuration est accessible dans le GUI.

Ce guide de configuration a été testé avec IPFire 2.27

!!! warning "C'est l'heure du Backup!"
    Avant d'apporter des modifications à un environnement de production, nous vous recommandons de [sauvegarder la configuration existante](https://wiki.ipfire.org/configuration/system/backup)

## Instructions

* Allez dans `System` -> `Domain Name System`
    * Sous `DNS Servers`, cliquez `Add`
        * Suivez ce processus deux fois, une pour chaque adresse IP Quad9, où le nom d'hôte TLS (hostname) sera toujours dns.quad9.net
            * IP address: `9.9.9.9`
            * IP address: `149.112.112.112`

* Utilisez les serveurs DNS attribués par le FAI: `Disabled`
* Protocole pour les requêtes DNS: `TLS`
* Activer la recherche sécurisée: `Disabled`
* Minimisation QNAME: `Disabled`
* Cliquez `Enregistrer`

## Verifier la Configuration

### GUI

Allez vers `Status` -> `Net-Traffic` dans le menu supérieur et recherchez une connexion active à `9.9.9.9` ou `149.112.112.112` via le port 853 TCP

### CLI

* Connectez-vous à votre materiel IPFire via SSH
* Installez le pack tshark

```
pakfire -y install tshark
```

* Démarrez un packet capture avec tshark afin de filtrer le trafique sur DNS over TLS:

```
tshark -i any 'port 853'
```

Si le materiel IPFire utilise DNS over HTTPS pour les requêtes DNS, you verrez ce type de résultat:
```
1 0.000000000 192.168.1.150 → 9.9.9.9 TCP 76 37226 → 853 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 SACK_PERM=1 TSval=3103990808 TSecr=0 WS=512
2 0.006914259 9.9.9.9 → 192.168.1.150 TCP 76 853 → 37226 [SYN, ACK] Seq=0 Ack=1 Win=28960 Len=0 MSS=1460 TSval=2447463919 TSecr=3103990808 WS=256
3 0.006948874 192.168.1.150 → 9.9.9.9 TCP 68 37226 → 853 [ACK] Seq=1 Ack=1 Win=64512 Len=0 TSval=3103990815 TSecr=2447463919
4 0.007110658 192.168.1.150 → 9.9.9.9 TLSv1 387 Client Hello
5 0.013306457 9.9.9.9 → 192.168.1.150 TCP 68 853 → 37226 [ACK] Seq=1 Ack=320 Win=30208 Len=0 TSval=2447463926 TSecr=3103990815
6 0.013926633 9.9.9.9 → 192.168.1.150 TLSv1.3 2964 Server Hello, Change Cipher Spec, Application Data
7 0.013945067 192.168.1.150 → 9.9.9.9 TCP 68 37226 → 853 [ACK] Seq=320 Ack=2897 Win=62464 Len=0 TSval=3103990822 TSecr=2447463926
```

Vous avez des questions? Vous rencontrez un probleme? Cela n'a pas marché? N'hésitez pas à nous contacter!

[Obtenir de l'aide](https://quad9.net/fr/support/contact){ .md-button .md-button--primary }
