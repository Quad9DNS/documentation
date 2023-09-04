Cloudflared is a DNS over HTTPS proxy that can be configured to use Quad9 for DNS resolution.

* In the `cloudflared.yml` configuration file, replace the Cloudflare IPs in the `proxy-dns-upstream` section with the Quad9 addresses associated with your desired features.
    * Restart the `cloudflared` service

Before (Cloudflare DoH Servers)
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

Questions? Issues? Didn't work? Contact us!

[Get Support](https://quad9.net/support/contact){ .md-button .md-button--primary }
