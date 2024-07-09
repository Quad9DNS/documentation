## Descripción general

Este artículo describe cómo configurar y usar Unbound en OpenBSD para enviar DNS cifrado a través de DNS sobre TLS a Quad9.

Esto fue probado usando OpenBSD 7.1.

!!! advertencia "Firefox, VPN"
     * **Firefox** está configurado para usar Cloudflare DNS de forma predeterminada en algunas regiones. Si está utilizando Firefox, verifique que [esto esté deshabilitado] (https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
     * **Las VPN** normalmente no respetan la configuración DNS del sistema o del enrutador. Si está utilizando una VPN, configure las direcciones IP de Quad9 en la configuración de "DNS personalizado" de su cliente VPN. Consulte la documentación de su proveedor de VPN para obtener más información.

!!! advertencia
     Unbound DNS se instala de forma predeterminada en instalaciones estándar de OpenBSD. Esto con la intención de actuar como un reenviador de DNS de almacenamiento en caché local solo para la máquina local, y no está destinado a actuar como un reenviador de DNS para otros dispositivos de red. Si desea ejecutar Unbound DNS en OpenBSD con el fin de ejecutar un reenviador DNS de almacenamiento en caché que será utilizado por múltiples dispositivos en la red, puede modificar apropiadamente la interfaz y los valores de control de acceso en unbound.conf, que de forma predeterminada, solo permitir consultas DNS desde localhost.

## Instrucciones

Debe iniciar sesión como usuario root directamente o ejecutando el comando `su` y escribiendo su contraseña en una sesión de Terminal.

* Haga una copia de seguridad del archivo unbound.conf predeterminado y descargue el archivo `unbound.conf` de reemplazo, que está preconfigurado para enviar consultas DNS a Quad9 a través de DNS sobre TLS.

!!! nota
     Le recomendamos descargar e inspeccionar el archivo unbound.conf en un editor de texto, que se adjunta a este artículo, antes de descargarlo a su sistema OpenBSD.
```
mv /var/unbound/etc/unbound.conf /var/unbound/etc/unbound.BAK && ftp -o /var/unbound/etc/unbound.conf https://docs.quad9.net/assets/conf/openbsd/unbound.conf
```

Opcional: si su red admite IPv6, abra el archivo /var/unbound/etc/unbound.conf en OpenBSD con su editor de texto favorito y realice los siguientes cambios, eliminando el # (comentario) antes de que comiencen estas líneas.

**Antes**

```
# do-ip6: no
# forward-addr: 2620:fe::fe@853#dns.quad9.net
# forward-addr: 2620:fe::9@853#dns.quad9.net
```

**Después**

```
do-ip6: yes
forward-addr: 2620:fe::fe@853#dns.quad9.net
forward-addr: 2620:fe::9@853#dns.quad9.net
```

* Configure Unbound para que se inicie al iniciar el sistema y habilite el servicio (ejecute estos comandos uno a la vez):

```
rcctl enable unbound
```
```
rcctl start unbound
```

## Verificar configuración

Abra una segunda sesión de Terminal separada para el sistema OpenBSD como usuario root e inicie una captura de paquetes, filtrando por el puerto 853 (puerto DNS sobre TLS):

tcpdump -n 'port 853'

* En su primera sesión de Terminal, asegúrese de que Unbound pueda responder consultas de DNS:

dig +short quad9.net @127.0.0.1

El resultado debe ser: 216.21.3.77
En su segunda sesión de Terminal, tcpdump debería mostrar un resultado como este, que confirma que la consulta DNS se envió a Quad9 con DNS sobre TLS:

```
tcpdump: listening on em0, link-type EN10MB
00:29:08.307240 192.168.1.194.42064 > 149.112.112.112.853: S 3620809840:3620809840(0) win 16384 <mss 1460,nop,nop,sackOK,nop,wscale 6,nop,nop,timestamp 495425124 0> (DF)
00:29:08.313467 149.112.112.112.853 > 192.168.1.194.42064: S 1684627303:1684627303(0) ack 3620809841 win 28960 <mss 1460,nop,nop,timestamp 3541989193 495425124,nop,wscale 8> (DF)
00:29:08.313559 192.168.1.194.42064 > 149.112.112.112.853: . ack 1 win 256 <nop,nop,timestamp 495425124 3541989193> (DF)
00:29:08.313895 192.168.1.194.42064 > 149.112.112.112.853: P 1:310(309) ack 1 win 256 <nop,nop,timestamp 495425124 3541989193> (DF)
00:29:08.319973 149.112.112.112.853 > 192.168.1.194.42064: . ack 310 win 118 <nop,nop,timestamp 3541989200 495425124> (DF)
00:29:08.320719 149.112.112.112.853 > 192.168.1.194.42064: . 1:1449(1448) ack 310 win 118 
```

Configure su sistema para comenzar a usar Unbound para DNS haciendo una copia de seguridad del archivo resolv.conf existente y configure 127.0.0.1 como servidor DNS para el sistema:
```
cp /etc/resolv.conf /etc/resolv.BAK && echo "nameserver 127.0.0.1" > /etc/resolv.conf
```

## Deshacer

Si desea dejar de usar Unbound como servidor DNS, simplemente restaure el archivo resolv.conf respaldado:

```
mv /etc/resolv.BAK /etc/resolv.conf
```

¿Preguntas? ¿Asuntos? ¿No funcionó? ¡Contáctenos!

[Obtener soporte](https://quad9.net/support/contact){ .md-button .md-button--primary }