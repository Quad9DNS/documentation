Quad9 ofrece varias variaciones de nuestro servicio DNS privado y gratuito.

## 9.9.9.9 (Seguro)

Nuestro servicio más popular. Un servicio DNS recursivo que bloquea amenazas y da prioridad a la privacidad.

| IPv4                        | IPv6                             | DNS sobre TLS    | DNS sobre HTTPS |
| --------------------------- | -------------------------------- | --------------- | -------------- |
| `9.9.9.9`, `149.112.112.112`| `2620:fe::fe`, `2620:fe::9`      | `dns.quad9.net` | `https://dns.quad9.net/dns-query` |

## 9.9.9.10 (Sin bloqueo de amenazas)

Para los usuarios que quieran aprovechar nuestro servicio DNS recursivo que prioriza la privacidad, pero no quieran bloquear amenazas, utilice nuestro servicio 9.9.9.10.

| IPv4                        | IPv6                             | DNS sobre TLS    | DNS sobre HTTPS |
| --------------------------- | -------------------------------- | --------------- | -------------- |
| `9.9.9.10`, `149.112.112.10`| `2620:fe::10`, `2620:fe::fe:10`  | `dns10.quad9.net` | `https://dns10.quad9.net/dns-query` |

## 9.9.9.11 (Seguro + ECS)

Para los usuarios que no se dirigen a la ubicación Quad9 más cercana posible, utilice nuestra versión 9.9.9.11 para obtener un mejor rendimiento de CDN:


| IPv4                        | IPv6                             | DNS sobre TLS    | DNS sobre HTTPS |
| --------------------------- | -------------------------------- | --------------- | -------------- |
| `9.9.9.11`, `149.112.112.11`| `2620:fe::11`, `2620:fe::fe:11`  | `dns11.quad9.net` | `https://dns11.quad9.net/dns-query` |

## 9.9.9.12 (Sin bloqueo de amenazas + ECS)

Para los usuarios que no se dirigen a la ubicación Quad9 más cercana posible y tampoco desean bloquear amenazas, utilice nuestra versión 9.9.9.12 para obtener un mejor rendimiento de CDN:

| IPv4                        | IPv6                             | DNS sobre TLS    | DNS sobre HTTPS |
| --------------------------- | -------------------------------- | --------------- | -------------- |
| `9.9.9.12`, `149.112.112.12`| `2620:fe::12`, `2620:fe::fe:12`  | `dns12.quad9.net` | `https://dns12.quad9.net/dns-query` |

## Puertos alternativos

Quad9 escucha en los siguientes puertos no estándar para una mejor disponibilidad de nuestros servicios en entornos de red restrictivos.

| Protocolo | Puerto estándar | Puerto alternativo
| --------------------------- | ------------------ | ------------- | 
| `UDP/TCP (Plaintext)`       | `53`               | `9953` | 
| `DNS sobre TLS`              | `853`              | `8853` |
| `DNS sobre HTTPS`            | `443`              | `5053` |
