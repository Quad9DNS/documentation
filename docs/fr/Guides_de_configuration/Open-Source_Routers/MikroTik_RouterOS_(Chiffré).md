## Aperçu

Cet article décrit comment configurer votre routeur MikroTik à l'aide de RouterOS pour envoyer des requêtes DNS chiffrées à Quad9 à l'aide de DNS over HTTPS.

RouterOS >=6.4.7 est requis. Ces instructions ont été testées en utilisant RouterOS 7.1.3.

!!! warning "C'est l'heure du Backup!"
    Avant d'apporter des modifications à un environnement de production, nous vous recommandons de [sauvegarder la configuration existante](https://help.mikrotik.com/docs/display/ROS/Backup)

## Instructions

* Connectez-vous à l'interface de gestion de votre routeur MikroTik via SSH ou la console. Le nom d'utilisateur et le mot de passe seront les mêmes que si vous utilisiez Webfig (GUI).

* Pour que MikroTik puisse effectuer la vérification du certificat du domaine Quad9 DNS over HTTPS, nous devons télécharger et importer le certificat DigiCert Global Root CA.
    * Téléchargez le certificat sur votre routeur MikroTik:

```
/tool/fetch mode=https url="https://cacerts.digicert.com/DigiCertGlobalG3TLSECCSHA3842020CA1-1.crt.pem"
```

* Importez le certificat dans la bibliothèque de certificats locale. Lorsque vous êtes invité à saisir une phrase secrète, appuyez simplement sur Entrée pour ne pas indiquer de phrase secrète:

```
/certificate/import file-name=DigiCertGlobalG3TLSECCSHA3842020CA1-1.crt.pem
```

Le résultat obtenu devrait être:

```
passphrase: 
certificates-imported: 1
private-keys-imported: 0
files-imported: 1
decryption-failures: 0
keys-with-no-certificate: 0
```

* Connectez vous dans Webfig (GUI), et allez dans `IP` -> `DNS` dans le menu de gauche.
*  Dans le champ `Servers` , entrez: `9.9.9.9`, `149.112.112.112`, `2620:fe::fe`, `2620:fe::9`

!!! warning

    Si votre réseau ne dispose pas d'IPv6, ce que vous pouvez vérifier ici, alors les adresses IPv6 ne doivent pas être ajoutées, car cela pourrait entraîner l'échec d'un nombre conséquent de vos requêtes DNS. [Test here](https://port.tools/ipv6-test/).

*  Use DoH Server: `https://dns.quad9.net/dns-query`
*  Verify DoH Certificate: `Enabled`
*  Allow Remote Requests: `Enabled`

!!! warning

    N'oubliez pas de configurer les règles de pare-feu pour empêcher une adresse IP non locale de l'utiliser comme serveur DNS.

8. Cliquez sur **Apply** en haut.

## Verifier la Configuration

Pour confirmer que le routeur MikroTik envoie des requêtes DNS à Quad9 en utilisant DNS over HTTPS, vous pouvez utiliser l'outil `packet sniffer` pour filtrer les paquets envoyés vers/depuis les adresses IP Quad9 en utilisant le port 443 (HTTPS):

```
tool/sniffer/quick port=443 ip-address=9.9.9.9,149.112.112.112
```

Si les requêtes DNS envoyées au routeur MikroTik sont transmises à Quad9 en utilisant DNS over HTTPS, vous verrez n'importe quelle sortie.

```
Columns: INTERFACE, TIME, NUM, DIR, SRC-MAC, DST-MAC, SRC-ADDRESS, DST-ADDRESS, PROTOCOL, SIZE, CPU
INTERFACE TIME NUM DIR SRC-MAC DST-MAC SRC-ADDRESS DST-ADDRESS PROTOCOL SIZE CPU
ether1 6.886 5 <- 04:F0:21:45:C9:0C 08:00:27:7D:3B:33 9.9.9.9:443 (https) 192.168.1.222:59348 ip:tcp 66 0
ether1 6.887 6 <- 04:F0:21:45:C9:0C 08:00:27:7D:3B:33 9.9.9.9:443 (https) 192.168.1.222:59348 ip:tcp 1514 0
ether1 6.887 7 -> 08:00:27:7D:3B:33 04:F0:21:45:C9:0C 192.168.1.222:59348 9.9.9.9:443 (https) ip:tcp 66 0
ether1 6.887 8 <- 04:F0:21:45:C9:0C 08:00:27:7D:3B:33 9.9.9.9:443 (https) 192.168.1.222:59348 ip:tcp 1514 0
ether1 6.887 9 -> 08:00:27:7D:3B:33 04:F0:21:45:C9:0C 192.168.1.222:59348 9.9.9.9:443 (https) ip:tcp 66 0
```

Si vous n'avez pas encore d'appareils utilisant le routeur MikroTik pour DNS, vous pouvez interroger manuellement le routeur MikroTik pour faciliter les tests et la vérification de la sortie générée ci-dessus à partir du terminal (Linux/macOS) ou de l'invite de commande (Windows), en remplaçant 192.168.1.1 par l'adresse IP LAN de votre routeur MikroTik.

```
nslookup quad9.net 192.168.1.1
```

Vous avez des questions? Vous rencontrez un probleme? Cela n'a pas marché? N'hésitez pas à nous contacter!

[Obtenir de l'aide](https://quad9.net/fr/support/contact){ .md-button .md-button--primary }
