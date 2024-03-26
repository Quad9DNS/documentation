## Descripción general

Android 9 y versiones posteriores incluyen la función "DNS privado", que le permite conectarse a servidores DNS mediante DNS sobre TLS (DoT). Es importante tener en cuenta que la función DNS privada no funciona si la aplicación Quad9 Connect está instalada y habilitada. Para configurar su dispositivo Android para usar Quad9 de esta manera, siga los pasos a continuación.

!!! advertencia "VPN"
     La función DNS privado no se utilizará si utiliza una VPN. Si utiliza una VPN, configure las direcciones IP de Quad9 en la configuración de "DNS personalizado" de su VPN. Consulte la documentación de su proveedor de VPN para obtener más información.

## Instrucciones

* Abra la aplicación :material-cog: `Ajustes` en su dispositivo Android.
     * Seleccione :material-wifi: `Conexión y compartir`.
         * Seleccione `DNS privado`.

* Seleccione `Nombre de host del provedor de DNS privado`
     * Ingrese: `dns.quad9.net`
         * Presione `Guardar`

## Verificar configuración

Visite [on.quad9.net](https://on.quad9.net) en el navegador de su elección.

¿Preguntas? ¿Asuntos? ¿No funcionó? ¡Contáctenos!

[Obtenga soporte](https://quad9.net/es/support/contact){ .md-button .md-button--primary }
