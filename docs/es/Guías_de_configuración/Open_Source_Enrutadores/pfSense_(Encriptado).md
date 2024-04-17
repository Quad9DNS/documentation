## Descripción general

pfSense es un firewall y enrutador de código abierto, utilizado tanto en entornos comerciales como de consumo.

pfSense tiene [documentación para DNS sobre TLS](https://docs.netgate.com/pfsense/en/latest/recipes/dns-over-tls.html), que recomendamos revisar además de este artículo.

pfSense utiliza Unbound, que tiene soporte DNS sobre TLS incorporado, y se puede acceder a la configuración en la GUI.

!!! advertencia "¡Tiempo de copia de seguridad!"
     Antes de realizar cambios en un entorno de producción, recomendamos [hacer una copia de seguridad de la configuración existente](https://docs.netgate.com/pfsense/en/latest/backup/configuration.html)
	 

## Instrucciones

Navegue hasta `System` -> `Generate Setup` en el menú superior.

* Haga clic en `Add DNS Server` hasta que haya 4 filas de entradas disponibles.
* Agregue las direcciones IPv4 e IPv6 de Quad9 en los campos de la izquierda:
`9.9.9.9`,`149.112.112.112`,`2620:fe::fe`,`2620:fe::9`

!!! advertencia
     Si su red no tiene IPv6, lo cual puede probar aquí, entonces no se deben agregar direcciones IPv6, ya que esto puede resultar en que un porcentaje de sus solicitudes de DNS fallen.

* Agregue `dns.quad9.net` en todos los campos de Hostname a la derecha.

Haga clic en `Save` en la parte inferior de la pantalla.

Navegue hasta `Services` -> `DNS Forwarder` en el menú superior.
* Asegúrese de que Enable DNS forwarder esté deshabilitado. Si está habilitado, desactívelo y haga clic en "Save" en la parte inferior de la página.

Navegue hasta `Services` -> `DNS Resolver` en el menú superior.

*Desplázate hacia abajo hasta encontrar la sección que se ve en la siguiente captura de pantalla.
* Desactive Enable DNSSEC Support  si está habilitado.
!!! nota "DNSSEC"
     Quad9 ya aplica DNSSEC y habilitar DNSSEC en el nivel del reenviador puede causar fallas falsas de DNSSEC.
* Habilitar `DNS Query Forwarding`
* Habilite `Use SSL/TLS for outgoing DNS queries to Forwarding Servers`
* Haga clic en "Save" en la parte inferior de la pantalla.
* Haga clic en "Apply Changes"  cerca de la parte superior de la pantalla para aplicar los cambios guardados.

## Verificar configuración

Puede confirmar que pfSense ahora envía sus consultas a través de DNS sobre TLS utilizando la herramienta de captura de paquetes incorporada.

También puede ejecutar una prueba desde un sistema macOS, Linux o Windows en la red.

[Obtenga soporte](https://quad9.net/es/support/contact){ .md-button .md-button--primary }
