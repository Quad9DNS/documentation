## Descripción general

IPFire es un firewall y enrutador de código abierto, utilizado tanto en entornos comerciales como de consumo.

IPFire utiliza Unbound, que tiene soporte DNS sobre TLS incorporado, y se puede acceder a la configuración en la GUI.

Esta guía de configuración fue probada usando IPFire 2.27

!!! advertencia "¡Tiempo de copia de seguridad!"
     Antes de realizar cambios en un entorno de producción, recomendamos [hacer una copia de seguridad de la configuración existente](https://wiki.ipfire.org/configuration/system/backup)

## Instrucciones

* Vaya a `System` -> `Domain Name System`
     * En `DNS Servers`, haga clic en `Add`	.
         * Realice este proceso dos veces, una para cada dirección IP de Quad9, donde el TLS Hostname siempre será dns.quad9.net
             * IP address `9.9.9.9`
             * IP address: `149.112.112.112`

* Use ISP-assigned DNS Servers: `Disabled`
* Protocol for DNS Queries: `TLS`
* Enable Safe Search: `Disabled`
* QNAME Minimisation: `Disabled`
* Haga clic en `Save`

## Verificar configuración

### GUI

Navegue hasta `Status` -> `Net-Traffic` en el menú superior y busque una conexión activa a `9.9.9.9` o `149.112.112.112` a través del puerto 853 TCP

### CLI

* Conéctese a su dispositivo IPFire a través de SSH
* Instale el paquete tshark

```
pakfire -y install tshark
```

* Inicie una captura de paquetes con tshark para filtrar el tráfico DNS sobre TLS:

```
tshark -i any 'port 853'
```

Si el dispositivo IPFire utiliza DNS sobre HTTPS para consultas de DNS, verá un resultado como este:

```
1 0.000000000 192.168.1.150 → 9.9.9.9 TCP 76 37226 → 853 [SYN] Seq=0 Win=64240 Len=0 MSS=1460 SACK_PERM=1 TSval=3103990808 TSecr=0 WS=512
2 0.006914259 9.9.9.9 → 192.168.1.150 TCP 76 853 → 37226 [SYN, ACK] Seq=0 Ack=1 Win=28960 Len=0 MSS=1460 TSval=2447463919 TSecr=3103990808 WS=256
3 0.006948874 192.168.1.150 → 9.9.9.9 TCP 68 37226 → 853 [ACK] Seq=1 Ack=1 Win=64512 Len=0 TSval=3103990815 TSecr=2447463919
4 0.007110658 192.168.1.150 → 9.9.9.9 TLSv1 387 Client Hello
5 0.013306457 9.9.9.9 → 192.168.1.150 TCP 68 853 → 37226 [ACK] Seq=1 Ack=320 Win=30208 Len=0 TSval=2447463926 TSecr=3103990815
6 0.013926633 9.9.9.9 → 192.168.1.150 TLSv1.3 2964 Server Hello, Change Cipher Spec, Application Data
7 0.013945067 192.168.1.150 → 9.9.9.9 TCP 68 37226 → 853 [ACK] Seq=320 Ack=2897 Win=62464 Len=0 TSval=3103990822 TSecr=2447463926
```

¿Preguntas? ¿Asuntos? ¿No funcionó? ¡Contáctenos!

[Obtenga soporte](https://quad9.net/support/contact){ .md-button .md-button--primary }