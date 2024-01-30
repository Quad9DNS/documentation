## Aperçu

Android 9 et les versions ultérieures incluent la fonctionnalité `DNS privé`, ce qui vous permet de vous connecter aux serveurs DNS en utilisant DNS over TLS (DoT). Il est important de noter que la fonction DNS privée ne fonctionnera pas si l'application Quad9 Connect est installée et activée. Pour configurer Quad9 sur votre appareil Android, suivez les étapes ci-dessous.

!!! warning "VPNs"
    La fonction DNS privé ne sera pas prise en compte avec un VPN actif. Si vous utilisez un VPN, vous devrez configurer l'adresse IP de Quad9 dans les paramètres `DNS personnalisé` de votre VPN. Veuillez vous référer à la documentation de votre fournisseur VPN pour plus d'informations.

## Instructions

* Ouvrez l'application :material-cog: `Paramètres` de votre appareil Android.
    * Selectionnez :material-wifi: `Connexions`.
        * Selectionnez `DNS privé`.

* Selectionnez `Nom d'hôte du fournisseur DNS privé`
    * Entrez: `dns.quad9.net`
        * Appuyez sur `Enregistrer`

## Verifier la Configuration

Allez sur [on.quad9.net](https://on.quad9.net) depuis le navigateur de votre choix.

Des questions? Des Problèmes? Cela n'a pas fonctionné ? N'hesitez pas à nous contacter!

[Obtenir de l'aide](https://quad9.net/fr/support/contact){ .md-button .md-button--primary }
