## Descripción general

Este artículo describe cómo configurar su enrutador MikroTik usando RouterOS para enviar consultas DNS cifradas a Quad9 usando DNS sobre HTTPS.

Se requiere RouterOS >=6.4.7. Estas instrucciones se probaron con RouterOS 7.1.3.

!!! advertencia "¡Tiempo de copia de seguridad!"
     Antes de realizar cambios en un entorno de producción, recomendamos [hacer una copia de seguridad de la configuración existente](https://help.mikrotik.com/docs/display/ROS/Backup)

## Instrucciones

* Conéctese a la interfaz de administración de su enrutador MikroTik a través de SSH o consola. El nombre de usuario y la contraseña serán los mismos que si usara Webfig (GUI).

* Para que MikroTik realice la verificación del certificado del DNS Quad9 sobre el dominio HTTPS, necesitamos descargar e importar el certificado DigiCert Global Root CA.
     * Descarga el certificado a tu router MikroTik:

```
/tool/fetch mode=https url="https://cacerts.digicert.com/DigiCertGlobalRootCA.crt.pem"
```

* Importe el certificado al almacén de certificados local. Cuando se le solicite una frase de contraseña, simplemente presione Intro para no tener contraseña:

```
/certificate/import file-name=DigiCertGlobalRootCA.crt.pem
```

El resultado debería ser:

```
passphrase: 
certificates-imported: 1
private-keys-imported: 0
files-imported: 1
decryption-failures: 0
keys-with-no-certificate: 0
```

* Inicie sesión en Webfig (GUI) y navegue hasta `IP` -> `DNS` en el menú del lado izquierdo.
* En el campo Servers, establezca: `9.9.9.9`, `149.112.112.112`, `2620:fe::fe`, `2620:fe::9`

!!! advertencia

     Si su red no es compatible con IPv6, entonces no se deben agregar las direcciones IPv6, ya que puede provocar que un porcentaje de sus solicitudes de DNS fallen. ¿No estás seguro de tener IPv6? [Pruebe aquí](https://port.tools/ipv6-test/).

*  Use DoH Server: `https://dns.quad9.net/dns-query`
*  Verify DoH Certificate: `Enabled`
*  Allow Remote Requests: `Enabled`

!!! advertencia

     No olvide configurar las reglas del firewall para evitar que una dirección IP no local la use como servidor DNS.

8. Haga clic en **Apply** en la parte superior.

### Verificar configuración

Para confirmar que el enrutador MikroTik está enviando consultas DNS a Quad9 usando DNS sobre HTTPS, puede usar la herramienta de rastreo de paquetes para filtrar los paquetes que se envían hacia/desde direcciones IP de Quad9 usando el puerto 443 (HTTPS):

```
herramienta/sniffer/puerto rápido=443 dirección-ip=9.9.9.9,149.112.112.112
```

Si las consultas de DNS enviadas al enrutador MikroTik se reenvían a Quad9 mediante DNS a través de HTTPS, verá cualquier resultado.

```
Columns: INTERFACE, TIME, NUM, DIR, SRC-MAC, DST-MAC, SRC-ADDRESS, DST-ADDRESS, PROTOCOL, SIZE, CPU
INTERFACE TIME NUM DIR SRC-MAC DST-MAC SRC-ADDRESS DST-ADDRESS PROTOCOL SIZE CPU
ether1 6.886 5 <- 04:F0:21:45:C9:0C 08:00:27:7D:3B:33 9.9.9.9:443 (https) 192.168.1.222:59348 ip:tcp 66 0
ether1 6.887 6 <- 04:F0:21:45:C9:0C 08:00:27:7D:3B:33 9.9.9.9:443 (https) 192.168.1.222:59348 ip:tcp 1514 0
ether1 6.887 7 -> 08:00:27:7D:3B:33 04:F0:21:45:C9:0C 192.168.1.222:59348 9.9.9.9:443 (https) ip:tcp 66 0
ether1 6.887 8 <- 04:F0:21:45:C9:0C 08:00:27:7D:3B:33 9.9.9.9:443 (https) 192.168.1.222:59348 ip:tcp 1514 0
ether1 6.887 9 -> 08:00:27:7D:3B:33 04:F0:21:45:C9:0C 192.168.1.222:59348 9.9.9.9:443 (https) ip:tcp 66 0
```

Si aún no tiene terminales que utilicen el enrutador MikroTik para DNS, puede consultar manualmente el enrutador MikroTik para facilitar las pruebas y la verificación de la salida generada anteriormente desde la Terminal (Linux/macOS) o el Símbolo del sistema (Windows), reemplazando 192.168.1.1 con la dirección IP LAN de su enrutador MikroTik.

```
nslookup quad9.net 192.168.1.1
```

[Obtenga soporte](https://quad9.net/support/contact){ .md-button .md-button--primary }