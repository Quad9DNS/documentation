### Descripción general

OPNsense es un firewall de código abierto, utilizado tanto en entornos comerciales como de consumo.

OPNsense utiliza Unbound, que tiene soporte DNS over TLS incorporado, y se puede acceder a la configuración en la GUI.

!!! warning "¡Tiempo de copia de seguridad!"
     Antes de realizar cambios en un entorno de producción, recomendamos [hacer una copia de seguridad de la configuración existente](https://docs.opnsense.org/manual/backups.html#backup)
	 
### Instrucciones

* Navegue a `Services` -> `Unbound DNS` -> `DNS over TLS`  en el menú del lado izquierdo
     * Haga clic en el botón +
         * Agregue 4 entradas, usando `dns.quad9.net` en el campo **Verify CN** y `853` en el campo **Server Port:**.

IP del servidor: `9.9.9.9`
IP del servidor: `149.112.112.112`
IP del servidor: `2620:fe::fe`
IP del servidor: `2620:fe::9`

!!! warning "IPv6"
     Si su red no tiene IPv6, lo cual puede probar aquí, entonces no se deben agregar direcciones IPv6, ya que esto puede resultar en que un porcentaje de sus solicitudes de DNS fallen.
	 
* Haga clic en "Aplicar" para guardar los cambios.

* Navegue a `System` -> `Settings` -> `General` en el menú del lado izquierdo.

* Desactivar `Allow DNS server list to be overridden by DHCP/PPP on WAN`
* Haga clic en `Save`
* Haga clic en "Apply" en la parte superior de la página.

### Verificar configuración

Para confirmar que OPNsense ahora envía sus consultas a través de DNS over TLS, puede ejecutar una captura de paquetes en la línea de comando, como por ejemplo:

```
tcpdump -i em0 'port 853'
```

!!! note
     Es posible que deba ajustar el nombre de la interfaz de em0 al de la interfaz WAN de su dispositivo.

También puede realizar la prueba desde un sistema macOS, Linux o Windows que esté conectado a este enrutador/firewall de OPNsense.

[Obtener soporte](https://quad9.net/support/contact){ .md-button .md-button--primary }
