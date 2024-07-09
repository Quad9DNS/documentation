## Descripción general

Este artículo describe cómo configurar y utilizar el servicio "local_unbound" preinstalado de FreeBSD para enviar DNS cifrado a través de DNS sobre TLS a Quad9.

Esto se probó con FreeBSD 13.1, pero debería funcionar también con 12.X.

!!! advertencia "Firefox, VPN"
     * **Firefox** está configurado para usar Cloudflare DNS de forma predeterminada en algunas regiones. Si está utilizando Firefox, verifique que [esto esté deshabilitado] (https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
     * **Las VPN** normalmente no respetan la configuración DNS del sistema o del enrutador. Si está utilizando una VPN, configure las direcciones IP de Quad9 en la configuración de "DNS personalizado" de su cliente VPN. Consulte la documentación de su proveedor de VPN para obtener más información.

!!! advertencia
     FreeBSD, de forma predeterminada, instala una instancia local de Unbound DNS. Esto con la intención de actuar como un reenviador de DNS de almacenamiento en caché local solo para la máquina local, y no está destinado a actuar como un reenviador de DNS para otros dispositivos de red. Si desea ejecutar Unbound DNS en FreeBSD con el fin de ejecutar un reenviador de DNS de almacenamiento en caché que será utilizado por múltiples dispositivos en la red, FreeBSD recomienda instalar el paquete dns/unbound en su lugar. Estas instrucciones sólo son válidas para el servicio "local_unbound".

## Instrucciones

Necesitará el comando sudo para ejecutar los siguientes comandos. Alternativamente, puede simplemente usar el comando su para convertirse en usuario root y ejecutar estos comandos directamente como usuario root, en cuyo caso deberá eliminar "sudo" de todos los comandos siguientes.

* Instale el comando dig para que pueda probar que la resolución DNS funciona como se esperaba:

```
pkg install bind-tools
```

* Verifique que local_unbound esté habilitado

```
sudo grep unbound /etc/rc.conf
```

Si se produce el siguiente resultado, local_unbound ya está habilitado y puede pasar a la siguiente sección:

```
local_unbound_enable="YES"
```

* Si no hay resultados después de este comando, entonces se debe habilitar local_unbound.
     * Indique al sistema que queremos usar local_unbound:
```
echo 'local_unbound_enable="YES"' >> /etc/rc.conf
```

Luego reinicie el sistema (sí, de verdad):

```
reboot
```

* Habilite local_unbound:

```
sudo local-unbound-setup
```

El resultado debería ser similar a este, pero puede diferir ligeramente:

```
destination: 
Extracting forwarders from /etc/resolv.conf.
/var/unbound/forward.conf not modified
/var/unbound/lan-zones.conf not modified
/var/unbound/control.conf not modified
/var/unbound/unbound.conf not modified
local_unbound not running? (check /var/run/local_unbound.pid).
Starting local_unbound.
/etc/resolvconf.conf created
Original /etc/resolv.conf saved as /var/backups/resolv.conf.20220625.200835
```

Configuración de local_unbound para DNS sobre TLS en Quad9

Este comando hará una copia de seguridad de los archivos de configuración predeterminados, descargará los archivos de configuración modificados del archivo adjunto de este artículo y reiniciará el servicio local_unbound.

```
sudo mv /var/unbound/forward.conf /var/unbound/forward-ORIG.conf && sudo mv /var/unbound/unbound.conf /var/unbound/unbound-ORIG.conf && sudo fetch -o /var/unbound/unbound.conf https://docs.quad9.net/assets/conf/freebsd/unbound.conf && sudo fetch -o /var/unbound/forward.conf https://docs.quad9.net/assets/conf/freebsd/forward.conf && sudo service local_unbound restart
```

Estos archivos están configurados para nuestro servicio 9.9.9.9 de forma predeterminada, sin IPv6. Si desea utilizar el servicio .10 o .11 y/o habilitar IPv6, abra el archivo `/var/unbound/forward.conf` y descomente/comente las líneas apropiadas.

## Verificar configuración

Necesitará dos sesiones/ventanas de Terminal

En la primera sesión, inicie una captura de paquetes para filtrar el tráfico DNS sobre TLS:
```
sudo tcpdump -n 'port 853'
```

En la segunda sesión, genere algunas búsquedas de DNS:

```
dig +short quad9.net && dig +short www.quad9.net && dig +short zombo.com
```

Vuelva a la primera sesión. Si ve algún resultado, su sistema ahora está usando DNS sobre TLS para enviar DNS cifrado a Quad9:

```
tcpdump: verbose output suppressed, use -v or -vv for full protocol decode
listening on em0, link-type EN10MB (Ethernet), capture size 262144 bytes
20:30:21.004625 IP 192.168.1.118.29017 > 149.112.112.112.853: Flags [S], seq 255439876, win 65535, options [mss 1460,nop,wscale 6,sackOK,TS val 2441683586 ecr 0], length 0
20:30:21.011088 IP 149.112.112.112.853 > 192.168.1.118.29017: Flags [S.], seq 838572319, ack 255439877, win 28960, options [mss 1460,nop,nop,TS val 3171725219 ecr 2441683586,nop,wscale 8], length 0
20:30:21.011140 IP 192.168.1.118.29017 > 149.112.112.112.853: Flags [.], ack 1, win 1027, options [nop,nop,TS val 2441683592 ecr 3171725219], length 0
20:30:21.011628 IP 192.168.1.118.29017 > 149.112.112.112.853: Flags [P.], seq 1:294, ack 1, win 1027, options [nop,nop,TS val 2441683592 ecr 3171725219], length 293
20:30:21.017885 IP 149.112.112.112.853 > 192.168.1.118.29017: Flags [.], ack 294, win 118, options [nop,nop,TS val 3171725226 ecr 2441683592], length 0
20:30:21.018447 IP 149.112.112.112.853 > 192.168.1.118.29017: Flags [.], seq 1:1449, ack 294, win 118, options [nop,nop,TS val 3171725227 ecr 2441683592], length 1448
20:30:21.018453 IP 149.112.112.112.853 > 192.168.1.118.29017: Flags [.], seq 1449:2897, ack 294, win 118, options [nop,nop,TS val 3171725227 ecr 2441683592], length 1448
```

## Deshacer

Para deshacer los cambios de configuración en local_unbound, simplemente ejecute este comando para restaurar los archivos originales y reiniciar local_unbound:

```
sudo mv /var/unbound/forward-ORIG.conf /var/unbound/forward.conf && sudo mv /var/unbound/unbound-ORIG.conf /var/unbound/unbound.conf && sudo service local_unbound restart
```

¿Preguntas? ¿Asuntos? ¿No funcionó? ¡Contáctenos!

[Obtener soporte](https://quad9.net/support/contact){ .md-button .md-button--primary }