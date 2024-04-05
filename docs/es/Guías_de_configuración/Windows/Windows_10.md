## Descripción general

La forma más sencilla de configurar Quad9 en toda su red es a través de la configuración de su enrutador. Si prefiere configurar Quad9 en un dispositivo Windows individual, siga los pasos a continuación para configurar Windows 10 para usar Quad9.

!!! advertencia "Firefox, VPN"
     * **Firefox** está configurado para usar Cloudflare DNS de forma predeterminada en algunas regiones. Si está utilizando Firefox, verifique que [esto esté deshabilitado](https://support.mozilla.org/es/kb/dns-sobre-https#w_configurar-la-proteccion-doh).
     * **Las VPN** normalmente no respetan la configuración DNS del sistema o del enrutador. Si está utilizando una VPN, configure las direcciones IP de Quad9 en la configuración de "DNS personalizado" de su cliente VPN. Consulte la documentación de su proveedor de VPN para obtener más información.
	 
## Instrucciones

### IPv4

* Haga clic derecho en el ícono de Red (por cable o WiFi) en la bandeja del sistema y haga clic en "Red e Internet".

* Haga clic en `Cambiar opciones del adaptador`

* Seleccione `Propiedades`.

* Seleccione `Protocolo de Internet versión 4 (TCP/IPv4)`. Luego, haga clic en "Propiedades".

* Seleccione `Usar las siguientes direcciones de servidor DNS`.
     * Ingrese: `9.9.9.9` en Servidor DNS preferido
     * Ingrese: `149.112.112.112` en el servidor DNS alternativo
* Haga clic en "Aceptar".

### IPv6

Si sus redes admiten IPv6, también se recomienda configurar las direcciones IPv6 de Quad9. Si no está seguro de si IPv6 está configurado en su red, puede probarlo aquí: https://test-ipv6.com/

* Seleccione `Protocolo de Internet versión 6 (TCP/IPv6) `
     * Haga clic en Propiedades.

* Seleccione  `Usar las siguientes direcciones de servidor DNS`.
     * Ingrese: `2620:fe::fe` en Servidor DNS preferido
     * Ingrese: `2620:fe::9` en el servidor DNS alternativo
         * Haga clic en "Aceptar".

*Cierre todas las ventanas de configuración.

## Verificar configuración

Confirme que está utilizando Quad9 visitando [on.quad9.net](https://on.quad9.net) en su navegador preferido.

¿Preguntas? ¿Asuntos? ¿No funcionó? ¡Contáctenos!

[Obtener soporte](https://quad9.net/es/support/contact){ .md-button .md-button--primary }
