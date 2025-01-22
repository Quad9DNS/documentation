## Descripción general

Siga los pasos a continuación para instalar el perfil DNS Quad9. Requiere iOS 14 o posterior.

!!! falla "VPN, iCloud Private Relay, Little Snitch"
     Cuando se utiliza iCloud Private Relay, la mayoría de los clientes VPN o Little Snitch, no utilizará ni respetará este perfil DNS.

     * **VPN**: no sigas estas instrucciones. En su lugar, configure las direcciones IP de Quad9 en la configuración "DNS personalizado" de su cliente VPN. Consulte la documentación de su cliente VPN para obtener más información.
   
     * **Apple Private Relay**: no sigas estas instrucciones. La retransmisión privada de Apple utilizará sus propios servidores DNS a nivel del sistema, sin forma de anularlos.
	 
## Elegir DNS over TLS o DNS over HTTPS

Se recomienda DNS over HTTPS para la mayoría de los usuarios. Si el dispositivo se conecta con frecuencia a Wi-Fi para invitados y/o redes que usted no administra.

Se recomienda DNS over TLS solo si el dispositivo se conectará principalmente a redes Wi-Fi que usted controla o a redes corporativas donde se permite DNS over TLS.

## Antes de que empieces

!!! tenga en cuenta "`nslookup` y `dig`"
     La App Store, así como los comandos `dig` y `nslookup` en una `Terminal` no utilizan DNS cifrado. Esto es por diseño.

!!! advertencia "DNS over TLS"
     Si está conectado a una red Wi-Fi que bloquea DNS a través de TLS, lo que puede ocurrir en firewalls de red restrictivos, tendrá que desactivar el perfil o desconectarse de la red para recuperar la resolución DNS. Esta solución no permite un comportamiento de "alternativa" sin cifrar. Se recomienda DNS over HTTPS para la mayoría de los usuarios.

!!! advertencia "¡Este perfil expirará!"
     Estos perfiles solo son válidos hasta que caduquen, momento en el cual se desactivarán automáticamente hasta que se instale un nuevo perfil. Esto es diseño de Apple y no hay forma de evitarlo.
	 
## Descargar perfil
Descargue uno de los perfiles aquí directamente usando Safari en su dispositivo iOS. Debes utilizar Safari para descargar el archivo.

!!! nota
     Si no sabe qué archivo elegir, le recomendamos **DNS over HTTPS - 9.9.9.9 (DNSSEC, bloqueo de amenazas)**
	 
* 9.9.9.9 (DNSSEC, bloqueo de amenazas)
    * [:fontawesome-solid-star:{ .heart } Recomendado: HTTPS (.9) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `b240f046a16f7d0e5df6458f5121221c4f118bf4d415cd8cce47d10b6fd46d36`
    * [TLS (.9) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `d132d71447bc3b43e371a86533e4d12fa46a4690a63abf77b2ceae72a1b3cef3`

* 9.9.9.10 (Sin DNSSEC,sin bloqueo de amenazas, Threat-Blocking)
    * [HTTPS (.10) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `42cb9445417dc81ced18c33d943c23559a81afb018d440bf465bb0635a44bb66`
    * [TLS (.10) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `86588f6d2dac42d03b155c7f557b4dd05b354059736aaa4ec8f3ef4d3ca2548e`

* 9.9.9.11 (DNSSEC, bloqueo de amenazas, con ECS)
    * [HTTPS (.11) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_ECS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `38c52f0755c4ec053c685e1ebf3b9956841a81373df2cc2e9dc962a418ac6993`
    * [TLS (.11) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_ECS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `abf69de093831cf8c4d644d234a3a594d13026415533ad1bb2b9f1540f307a46`

* 9.9.9.12 (Sin DNSSEC, sin bloqueo de amenazas, con ECS)
    * [HTTPS (.12) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_ECS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `eccb63252a1cd6726d42a1d72c58e11503cf06a0de6977d2472386f9cc88d9d8`
    * [TLS (.12) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_ECS_20260126.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `0b01df454c9e4ee7f39b0a79e63920c6fa6e44f1fe17c0064bb8da6ce68bcb04`

## Instalación

* Navegue a su carpeta de Descargas y seleccione el perfil que acaba de descargar.
     * Abra `Ajustes` > `Perfil descargado` y seleccione el perfil Quad9 que abrió.
         * Haga clic en "Instalar".
             * Ingrese la contraseña de su teléfono.
!!! nota
     Recibirá un mensaje de advertencia advirtiéndole que el servidor DNS puede filtrar o monitorear el tráfico de su red. Si bien el perfil de Quad9 puede proteger su dispositivo al filtrar el tráfico potencialmente malicioso, Quad9 no registrará nada de su tráfico. Consulte nuestra [Política de privacidad](https://quad9.net/es/service/privacy) para obtener más información.
	 
* Seleccione `Instalar`, luego `Instalar` nuevamente.

* El perfil ya está instalado. Seleccione "Hecho".

## Verificar configuración

Para confirmar que la instalación fue exitosa, visite [on.quad9.net](https://on.quad9.net)

¿Preguntas? ¿Asuntos? ¿No funcionó? ¡Contáctenos!

[Obtenga soporte](https://quad9.net/es/support/contact){ .md-button .md-button--primary }
