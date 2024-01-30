Quad9 propose plusieurs variantes de notre service DNS privé et gratuit.

## 9.9.9.9 (Sécurisé)

Notre service le plus populaire. Un service DNS confidentiel, récursif, contre les menaces.

| IPv4                        | IPv6                             | DNS over TLS    | DNS over HTTPS |
| --------------------------- | -------------------------------- | --------------- | -------------- |
| `9.9.9.9`, `149.112.112.112`| `2620:fe::fe`, `2620:fe::9`      | `dns.quad9.net` | `https://dns.quad9.net/dns-query` |

## 9.9.9.10 (Pas de blocage des menaces)

Pour les utilisateurs qui souhaitent profiter de notre service DNS récursif et confidentiel, mais qui ne souhaitent pas bloquer les menaces, utilisez plutôt notre service 9.9.9.10. 

| IPv4                        | IPv6                             | DNS over TLS    | DNS over HTTPS |
| --------------------------- | -------------------------------- | --------------- | -------------- |
| `9.9.9.10`, `149.112.112.10`| `2620:fe::10`, `2620:fe::fe:10`  | `dns10.quad9.net` | `https://dns10.quad9.net/dns-query` |

## 9.9.9.11 (Securisé + ECS)

Pour les utilisateurs qui ne souhaitent pas router vers l'emplacement Quad9 le plus proche, utilisez 9.9.9.11 pour de meilleures performances CDN:


| IPv4                        | IPv6                             | DNS over TLS    | DNS over HTTPS |
| --------------------------- | -------------------------------- | --------------- | -------------- |
| `9.9.9.11`, `149.112.112.11`| `2620:fe::11`, `2620:fe::fe:11`  | `dns11.quad9.net` | `https://dns11.quad9.net/dns-query` |

## 9.9.9.12 (Pas de blocage des menaces + ECS)

Pour les utilisateurs qui ne souhaitent pas router vers l'emplacement Quad9 le plus proche, et qui ne souhaitent pas bloquer les menaces, utilisez 9.9.9.12 pour de meilleures performances CDN:

| IPv4                        | IPv6                             | DNS over TLS    | DNS over HTTPS |
| --------------------------- | -------------------------------- | --------------- | -------------- |
| `9.9.9.12`, `149.112.112.12`| `2620:fe::12`, `2620:fe::fe:12`  | `dns12.quad9.net` | `https://dns12.quad9.net/dns-query` |

## Ports alternatifs

Quad9 propose les ports non standard suivants pour une meilleure disponibilité de nos services dans des environnements réseau restrictifs.

| Protocol                    | Standard Port      | Alternate Port 
| --------------------------- | ------------------ | ------------- | 
| `UDP/TCP (Plaintext)`       | `53`               | `9953` | 
| `DNS over TLS`              | `853`              | `8853` |
| `DNS over HTTPS`            | `443`              | `5053` |
