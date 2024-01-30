Cloudflared est un proxy DNS over HTTPS qui peut être configuré pour utiliser Quad9 pour la résolution DNS.

* Dans le fichier de configuration `cloudflared.yml` , remplacez les IP Cloudflare dans la section `proxy-dns-upstream` par les adresses Quad9 associées aux fonctionnalités souhaitées.
     * Redémarrez le service `cloudflared`

Avant (Cloudflare DNS over HTTP Servers)
```
proxy-dns-upstream:

- https://1.1.1.1/dns-query
- https://1.0.0.1/dns-query
```

IPv4
```
proxy-dns-upstream:

- https://9.9.9.9/dns-query
- https://149.112.112.112/dns-query
```

IPv6
```
proxy-dns-upstream:

- https://[2620:fe::fe]/dns-query
- https://[2620:fe::9]/dns-query
```

Vous avez des questions? Vous rencontrez un probleme? Cela n'a pas marché? N'hésitez pas à nous contacter!

[Obtenir de l'aide](https://quad9.net/fr/support/contact){ .md-button .md-button--primary }
