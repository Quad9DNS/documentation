## Descripción general

Nota: Los mantenedores de systemd-resolved enfatizan que esta implementación de DNS sobre TLS es actualmente un trabajo en progreso. Puedes considerar usar Stubby en su lugar si experimentas problemas de rendimiento. Consulte aquí las instrucciones de Ubuntu 18.04/20.04 + Stubby.

Ubuntu 22.04 y Linux Mint 20.3 o posterior admiten DNS sobre TLS de forma nativa en systemd-resolved, pero la opción no está disponible en la GUI.

!!! bicho
     Si bien esto también es técnicamente compatible con Ubuntu *20.04*, no recomendamos usar este método para 20.04, ya que utiliza una versión anterior de systemd-resolve que tiene problemas.

!!! bicho
     La opción DNSSEC no debe estar habilitada en systemd-resolved. Tiene muchos errores y solo duplicaría el proceso de validación DNSSEC que ya realiza Quad9, lo que reduce significativamente el rendimiento.

!!! advertencia "Firefox, VPN"
     * **Firefox** está configurado para usar Cloudflare DNS de forma predeterminada en algunas regiones. Si está utilizando Firefox, verifique que [esto esté deshabilitado] (https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
     * **Las VPN** normalmente no respetan la configuración DNS del sistema o del enrutador. Si está utilizando una VPN, configure las direcciones IP de Quad9 en la configuración de "Custom DNS" de su cliente VPN. Consulte la documentación de su proveedor de VPN para obtener más información.

## Instrucciones

* Configure Quad9 en la Configuración de red ([Ubuntu](editme), [Linux Mint](editme)).

* Abra la aplicación `Terminal` y copie y pegue estos comandos para habilitar DNS sobre TLS. Cuando se le solicite su contraseña, escríbala y presione "Enter".

```
sudo sed -i 's/#DNSOverTLS=no/DNSOverTLS=yes/g' /etc/systemd/resolved.conf
```

* Reinicie `systemd-resolvd` y `networking services` para reconocer los cambios en el archivo:

```
sudo systemctl restart systemd-resolved.service && sudo service network-manager restart
```
## Verificar configuración

* Confirme que se está utilizando DNS sobre TLS abriendo la aplicación `Terminal` y ejecutando el siguiente comando, escribiendo su contraseña y presionando `Enter`:

```
$ dig +short txt proto.on.quad9.net.

```
Si la respuesta es `dot.`, ¡entonces está funcionando! Si la respuesta es `do53-udp.`, entonces todavía está usando texto sin formato. Si no hay respuesta, eso significa que es posible que Quad9 no se haya configurado probablemente en la `Network Settings`.

## Deshacer

Si experimenta algún problema o desea deshacer este cambio de configuración:

* Abra la aplicación Terminal y copie/pegue estos comandos para deshabilitar DNS sobre TLS. Se le pedirá su contraseña.

```
sudo sed -i 's/DNSOverTLS=yes/#DNSOverTLS=no/g' /etc/systemd/resolved.conf
```

* Reinicie los servicios `systemd-resolvd` y `networking` para reconocer los cambios en el archivo que acabamos de realizar:

```
sudo systemctl restart systemd-resolved.service && sudo service network-manager restart
```

¿Preguntas? ¿Asuntos? ¿No funcionó? ¡Contáctenos!

[Obtener soporte](https://quad9.net/support/contact){ .md-button .md-button--primary }
