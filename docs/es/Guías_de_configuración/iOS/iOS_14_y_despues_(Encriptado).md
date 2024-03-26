## Descripción general

Siga los pasos a continuación para instalar el perfil DNS Quad9. Requiere iOS 14 o posterior.

!!! falla "VPN, iCloud Private Relay, Little Snitch"
     Cuando se utiliza iCloud Private Relay, la mayoría de los clientes VPN o Little Snitch, no utilizará ni respetará este perfil DNS.

     * **VPN**: no sigas estas instrucciones. En su lugar, configure las direcciones IP de Quad9 en la configuración "DNS personalizado" de su cliente VPN. Consulte la documentación de su cliente VPN para obtener más información.
   
     * **Apple Private Relay**: no sigas estas instrucciones. La retransmisión privada de Apple utilizará sus propios servidores DNS a nivel del sistema, sin forma de anularlos.
	 
## Elegir DNS sobre TLS o DNS sobre HTTPS

Se recomienda DNS sobre HTTPS para la mayoría de los usuarios. Si el dispositivo se conecta con frecuencia a Wi-Fi para invitados y/o redes que usted no administra.

Se recomienda DNS sobre TLS solo si el dispositivo se conectará principalmente a redes Wi-Fi que usted controla o a redes corporativas donde se permite DNS sobre TLS.

## Antes de que empieces

!!! tenga en cuenta "`nslookup` y `dig`"
     La App Store, así como los comandos `dig` y `nslookup` en una `Terminal` no utilizan DNS cifrado. Esto es por diseño.

!!! advertencia "DNS over TLS"
     Si está conectado a una red Wi-Fi que bloquea DNS a través de TLS, lo que puede ocurrir en firewalls de red restrictivos, tendrá que desactivar el perfil o desconectarse de la red para recuperar la resolución DNS. Esta solución no permite un comportamiento de "alternativa" sin cifrar. Se recomienda DNS sobre HTTPS para la mayoría de los usuarios.

!!! advertencia "This profile will expire!"
     Estos perfiles solo son válidos hasta que caduquen, momento en el cual se desactivarán automáticamente hasta que se instale un nuevo perfil. Esto es diseño de Apple y no hay forma de evitarlo.
	 
## Descargar perfil
Descargue uno de los perfiles aquí directamente usando Safari en su dispositivo iOS. Debes utilizar Safari para descargar el archivo.

!!! nota
     Si no sabe qué archivo elegir, le recomendamos **DNS sobre HTTPS - 9.9.9.9 (DNSSEC, bloqueo de amenazas)**
	 
* 9.9.9.9 (DNSSEC, Threat-Blocking)
    * [DNS over TLS - 9.9.9.9](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_20250129.mobileconfig) (Expires Jan 29, 2025)
    * [DNS over HTTPS - 9.9.9.9](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_20250129.mobileconfig) (Expires Jan 29, 2025)

* 9.9.9.10 (No DNSSEC, no Threat-Blocking)
    * [DNS over TLS - 9.9.9.10](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_20250129.mobileconfig) (Expires Jan 29, 2025)
    * [DNS over HTTPS  - 9.9.9.10](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_20250129.mobileconfig) (Expires Jan 29, 2025)

* 9.9.9.11 (DNSSEC, Threat-Blocking, with ECS)
    * [DNS over TLS - 9.9.9.11](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_TLS_ECS_20250129.mobileconfig) (Expires Jan 29, 2025)
    * [DNS over HTTPS - 9.9.9.11](https://docs.quad9.net/assets/mobileconfig/Quad9_Secured_DNS_over_HTTPS_ECS_20250129.mobileconfig) (Expires Jan 29, 2025)

* 9.9.9.12 (No DNSSEC, no Threat-Blocking, with ECS)
    * [DNS over TLS - 9.9.9.12](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_TLS_ECS_20250129.mobileconfig) (Expires Jan 29, 2025)
    * [DNS over HTTPS - 9.9.9.12](https://docs.quad9.net/assets/mobileconfig/Quad9_un_Secured_DNS_over_HTTPS_ECS_20250129.mobileconfig) (Expires Jan 29, 2025) 

## Instalación

* Navegue a su carpeta de Descargas y seleccione el perfil que acaba de descargar.
     * Abra `Settings` > `Profile Downloaded` y seleccione el perfil Quad9 que abrió.
         * Haga clic en "Install".
             * Ingrese la contraseña de su teléfono.
!!! nota
     Recibirá un mensaje de advertencia advirtiéndole que el servidor DNS puede filtrar o monitorear el tráfico de su red. Si bien el perfil de Quad9 puede proteger su dispositivo al filtrar el tráfico potencialmente malicioso, Quad9 no registrará nada de su tráfico. Consulte nuestra [Política de privacidad](https://quad9.net/service/privacy) para obtener más información.
	 
* Seleccione `Install`, luego `Install` nuevamente.

* El perfil ya está instalado. Seleccione "Done".

## Verificar configuración

Para confirmar que la instalación fue exitosa, visite [on.quad9.net](https://on.quad9.net)

¿Preguntas? ¿Asuntos? ¿No funcionó? ¡Contáctenos!

[Obtenga soporte](https://quad9.net/support/contact){ .md-button .md-button--primary }