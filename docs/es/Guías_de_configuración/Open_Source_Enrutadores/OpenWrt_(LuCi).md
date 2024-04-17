## Descripción general

El Proyecto OpenWrt es un sistema operativo Linux dirigido a dispositivos integrados, que a menudo se utiliza como una solución de código abierto para enrutadores y firewalls.

Esta guía cubre la configuración de Quad9 en la configuración del reenviador DNS. Cuando utilice su enrutador OpenWrt como servidor DNS, reenviará las solicitudes de DNS a Quad9.

!!! advertencia "¡Tiempo de copia de seguridad!"
     Antes de realizar cambios en un entorno de producción, recomendamos [hacer una copia de seguridad de la configuración existente](https://openwrt.org/docs/guide-user/troubleshooting/backup_restore)

## Instrucciones

* Inicie sesión en su panel de control de LuCI, normalmente abriendo `http://192.168.1.1` en su navegador.

* Navegue a ``Network` -> `DHCP and DNS`
     * Configure `9.9.9.9` y `149.112.112.112`, o las direcciones de su servicio Quad9 preferido en los campos de entrada "DNS forwardings".

* Si su red admite IPv6, también puede agregar 2620:fe::fe y 2620:fe::9, o las direcciones IPv6 de su servicio Quad9 preferido.

* Navegue a la subpestaña `Resolv and Hosts Files` y asegúrese de que "`Ignore resolv file`" esté "enabled".

* Haga clic en Save & Apply` en la parte inferior. Dado que no está cambiando la configuración de DHCP, el cambio debería ser instantáneo.

## Verificar configuración

* Confirma que estás usando Quad9 en Linux, MacOS o Windows.

[Obtenga soporte](https://quad9.net/es/support/contact){ .md-button .md-button--primary }
