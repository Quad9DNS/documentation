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
    * [:fontawesome-solid-star:{ .heart } Recomendado: HTTPS (.9) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `2fd22c5ca55ba2404a63f28a9cb4e25545194989a929895b3a689be232e62871`
    * [TLS (.9) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `56af33fe8d1e0f55d429f826fa9822a0a97a8aeb7ad28cca82b26536753d8132`

* 9.9.9.10 (Sin DNSSEC,sin bloqueo de amenazas, Threat-Blocking)
    * [HTTPS (.10) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `ef18da540f7c30a3e9e0e7c4a40c3cde29791da0e02b9851f0195099383c901f`
    * [TLS (.10) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `6a76af77beace68de0a3ad3b4847eeff3f90eca60a2a7a01fd3063f2366f764c`

* 9.9.9.11 (DNSSEC, bloqueo de amenazas, con ECS)
    * [HTTPS (.11) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_ECS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `1212594f9919783167338ea7d1797e8532e4b1426d58e0324983499c8c68dfc2`
    * [TLS (.11) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_ECS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `43a8da875650c899ce8ba6005040fca520951803bd9a02141ef7815cd164f785`

* 9.9.9.12 (Sin DNSSEC, sin bloqueo de amenazas, con ECS)
    * [HTTPS (.12) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_ECS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `f5b2d174c7096b976af1c59df9c2423126ef59d96ae3fa2a8a3138907f910f2d`
    * [TLS (.12) :fontawesome-solid-download:](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_ECS_20260119.mobileconfig){ .md-button .md-button--primary }
        * SHA256: `beb4610573f73d5fb524594530f07107000eb352b804f39ef84b226a8b75ab85`

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
