Quad9 oferă mai multe variante ale serviciului nostru DNS gratuit și privat.

## 9.9.9.9 (Securizat)

Cel mai popular serviciu al nostru. Un serviciu DNS recursiv care blochează amenințările și ține cont în primul rând de confidențialitate.

| IPv4                        | IPv6                             | DNS over TLS    | DNS over HTTPS |
| --------------------------- | -------------------------------- | --------------- | -------------- |
| `9.9.9.9`, `149.112.112.112`| `2620:fe::fe`, `2620:fe::9`      | `dns.quad9.net` | `https://dns.quad9.net/dns-query` |

## 9.9.9.10 (Fără blocarea amenințărilor)

Pentru utilizatorii care doresc să profite de serviciul nostru DNS recursiv bazat pe confidențialitate, dar nu doresc blocarea amenințărilor, utilizați în schimb serviciul nostru 9.9.9.10. 

| IPv4                        | IPv6                             | DNS over TLS    | DNS over HTTPS |
| --------------------------- | -------------------------------- | --------------- | -------------- |
| `9.9.9.10`, `149.112.112.10`| `2620:fe::10`, `2620:fe::fe:10`  | `dns10.quad9.net` | `https://dns10.quad9.net/dns-query` |

## 9.9.9.11 (Securizat + ECS)

Pentru utilizatorii care nu direcționează către cea mai apropiată locație Quad9 posibilă, utilizați 9.9.9.11 pentru o performanță CDN mai bună:

| IPv4                        | IPv6                             | DNS over TLS    | DNS over HTTPS |
| --------------------------- | -------------------------------- | --------------- | -------------- |
| `9.9.9.11`, `149.112.112.11`| `2620:fe::11`, `2620:fe::fe:11`  | `dns11.quad9.net` | `https://dns11.quad9.net/dns-query` |

## 9.9.9.12 (Fără blocarea amenințărilor + ECS)

Pentru utilizatorii care nu direcționează către cea mai apropiată locație Quad9 posibilă și care, de asemenea, nu doresc blocarea amenințărilor, utilizați versiunea noastră 9.9.9.12 pentru o performanță CDN mai bună:

| IPv4                        | IPv6                             | DNS over TLS    | DNS over HTTPS |
| --------------------------- | -------------------------------- | --------------- | -------------- |
| `9.9.9.12`, `149.112.112.12`| `2620:fe::12`, `2620:fe::fe:12`  | `dns12.quad9.net` | `https://dns12.quad9.net/dns-query` |

## Porturi alternative

Quad9 ascultă pe următoarele porturi non-standard pentru o mai bună disponibilitate a serviciilor noastre în medii de rețea restrictive:

| Protocol                    | Standard Port      | Alternate Port 
| --------------------------- | ------------------ | ------------- | 
| `UDP/TCP (Plaintext)`       | `53`               | `9953` | 
| `DNS over TLS`              | `853`              | `8853` |
| `DNS over HTTPS`            | `443`              | `5053` |
