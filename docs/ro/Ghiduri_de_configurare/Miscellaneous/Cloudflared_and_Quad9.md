Cloudflared este un proxy DNS over HTTPS care poate fi configurat pentru a utiliza Quad9 pentru rezoluția DNS.

* În fișierul de configurare `cloudflared.yml`, înlocuiți IP-urile Cloudflare din secțiunea `proxy-dns-upstream` cu adresele Quad9 asociate cu caracteristicile dorite.
    * Reporniți serviciul `cloudflared`.

Înainte (Cloudflare DoH Servers)
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

Întrebări? Probleme? Nu a funcționat? Contactați-ne!

[Obțineți asistență](https://quad9.net/support/contact){ .md-button .md-button--primary }
