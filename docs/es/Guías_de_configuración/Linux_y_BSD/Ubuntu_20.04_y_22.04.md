## Descripción general

La forma más sencilla de configurar Quad9 en toda su red es a través de la configuración de su enrutador. Si prefiere configurar Quad9 en un solo sistema, siga los pasos a continuación para configurar Ubuntu 22.04 o 22.04 LTS para usar Quad9.

!!! advertencia "Firefox, VPN"
     * **Firefox** está configurado para usar Cloudflare DNS de forma predeterminada en algunas regiones. Si está utilizando Firefox, verifique que [esto esté deshabilitado] (https://support.mozilla.org/en-US/kb/dns-over-https#w_configure-doh-protection-settings).
     * **Las VPN** normalmente no respetan la configuración DNS del sistema o del enrutador. Si está utilizando una VPN, configure las direcciones IP de Quad9 en la configuración de "DNS personalizado" de su cliente VPN. Consulte la documentación de su proveedor de VPN para obtener más información.

## Instrucciones

### IPv4

* Desde el escritorio de Ubuntu, seleccione el menú desplegable en la esquina superior derecha de la pantalla, expanda "Wired Connection" o "Wireless Connection" según su tipo de conexión, luego seleccione "Wired Setting" o "Wireless Settings".

* Haga clic en el icono :gear: junto a su conexión.

* Haga clic en la pestaña `IPv4`
     * Desactivar `Automatic DNS`
         * Ingrese las direcciones IP Quad9 de su servicio preferido.

Se pueden ingresar varias direcciones IP en la lista usando comas.

`9.9.9.9, 149.112.112.112`

* Si no va a utilizar IPv6, haga clic en "Apply" para completar el proceso de configuración y luego confirme que está utilizando Quad9.


### IPv6 (opcional)

Si su red/computadora admite IPv6, también se recomienda configurar las direcciones IPv6 de Quad9. Si no está seguro de si IPv6 está configurado en su red, puede probarlo aquí: https://test-ipv6.com/


* Select the `IPv6` tab
    * Desactivar `Automatic DNS`
        * Ingrese las direcciones IP Quad9 de su servicio preferido.

Se pueden ingresar varias direcciones IP en la lista usando comas.

`2620:fe::fe, 2620:fe::9`

* Haga clic en "Apply" para completar el proceso de configuración.

## Verificar configuración

Confirme que está utilizando Quad9 visitando [on.quad9.net](https://on.quad9.net) en su navegador preferido.

¿Preguntas? ¿Asuntos? ¿No funcionó? ¡Contáctenos!

[Obtener soporte](https://quad9.net/support/contact){ .md-button .md-button--primary }