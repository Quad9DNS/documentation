Cloudflared es un proxy DNS sobre HTTPS que se puede configurar para usar Quad9 para la resolución de DNS.

* En el archivo de configuración `cloudflared.yml`, reemplace las IP de Cloudflare en la sección `proxy-dns-upstream` con las direcciones Quad9 asociadas con las funciones que desee.
     * Reinicie el servicio `cloudflared`
	 
Antes (servidores DoH de Cloudflare)
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

¿Preguntas? ¿Asuntos? ¿No funcionó? ¡Contáctenos!

[Obtenga soporte](https://quad9.net/support/contact){ .md-button .md-button--primary }