Quad9 offers several variations of our free, private DNS service.

## 9.9.9.9 (Secure)

Our most-popular service. A threat-blocking, privacy-first recursive DNS service.

| IPv4                        | IPv6                             | DNS over TLS    | DNS over HTTPS |
| --------------------------- | -------------------------------- | --------------- | -------------- |
| `9.9.9.9`, `149.112.112.112`| `2620:fe::fe`, `2620:fe::9`      | `dns.quad9.net` | `https://dns.quad9.net/dns-query` |

## 9.9.9.10 (No Threat Blocking)

For users who want to take advantage of our privacy-first recursive DNS service, but do not want threat blocking, use our 9.9.9.10 service instead. 

| IPv4                        | IPv6                             | DNS over TLS    | DNS over HTTPS |
| --------------------------- | -------------------------------- | --------------- | -------------- |
| `9.9.9.10`, `149.112.112.10`| `2620:fe::10`, `2620:fe::fe:10`  | `dns10.quad9.net` | `https://dns10.quad9.net/dns-query` |

## 9.9.9.11 (Secure + ECS)

For users who do not route to the closest-possible Quad9 location, use our 9.9.9.11 for better CDN performance:


| IPv4                        | IPv6                             | DNS over TLS    | DNS over HTTPS |
| --------------------------- | -------------------------------- | --------------- | -------------- |
| `9.9.9.11`, `149.112.112.11`| `2620:fe::11`, `2620:fe::fe:11`  | `dns11.quad9.net` | `https://dns11.quad9.net/dns-query` |

## 9.9.9.12 (No Threat Blocking + ECS)

For users who do not route to the closest-possible Quad9 location, and also do not want threat blocking, use our 9.9.9.12 for better CDN performance:

| IPv4                        | IPv6                             | DNS over TLS    | DNS over HTTPS |
| --------------------------- | -------------------------------- | --------------- | -------------- |
| `9.9.9.12`, `149.112.112.12`| `2620:fe::12`, `2620:fe::fe:12`  | `dns12.quad9.net` | `https://dns12.quad9.net/dns-query` |

## Alternate Ports

Quad9 listens on the following, non-standard ports for better availability of our services in restrictive networking environments.

| Protocol                    | Standard Port      | Alternate Port 
| --------------------------- | ------------------ | ------------- | 
| `UDP/TCP (Plaintext)`       | `53`               | `9953` | 
| `DNS over TLS`              | `853`              | `8853` |
| `DNS over HTTPS`            | `443`              | `5053` |
