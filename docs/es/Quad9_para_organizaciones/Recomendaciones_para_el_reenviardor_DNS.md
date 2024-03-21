## Descripción general

Estás administrando DNS para un edificio, oficina, empresa, ISP, etc., y deseas utilizar Quad 9. ¡Excelente elección!

!!! nota

	Para ISP u organizaciones con más de 5000 usuarios detrás de una caché de reenvío, o si espera más de 500 consultas por segundo desde una única dirección IP de salida, comuníquese con [Soporte de Quad9](https://quad9.net/support/contact) con los detalles de su implementación, y asi poder trabajar juntos para garantizar una implementación fluida y exitosa.

Los reenviadores de caché y su configuración óptima son fundamentales cuando se envían consultas en masa a Quad9, y es muy preferible a la asignación directa a través de DHCP a los usuarios finales con respecto a:

### Desempeño
Reducir la cantidad de consultas que recurren a Quad9, ahorrar ancho de banda y brindar una experiencia más rápida para el usuario final cuando sus consultas ya están en la memoria caché de los reenviadores.

### Seguridad
Se recomienda habilitar el registro de consultas o algún tipo de métrica de alto nivel para identificar posibles compromisos de puntos finales o clientes específicos y, en ocasiones, lo exige la ley local.

### Política local
Poder bloquear o analizar ciertos FQDN en el nivel del reenviador pone más control en manos del administrador de la red sin depender exclusivamente de Quad9 para bloquear dominios maliciosos.

Al configurar Quad9 como solucionador recursivo en su infraestructura y almacenar en caché los reenviadores de DNS, considere las siguientes recomendaciones.

### Exclusividad

Dado que los reenviadores de DNS utilizan ordenamiento por turnos al reenviar consultas a una lista de servidores DNS recursivos, Quad9 debe configurarse como los servidores DNS recursivos exclusivos en sus reenviadores. Agregar servidores DNS recursivos adicionales que no sean Quad9 dará como resultado que un porcentaje de sus consultas DNS no estén protegidas por el bloqueo de amenazas de Quad9.

### Almacenamiento en caché

Es imperativo que sus reenviadores DNS estén configurados para almacenar en caché los datos de respuesta para evitar consultas recursivas excesivas a Quad9 y proporcionar una resolución DNS significativamente más rápida para los dispositivos en la red.

Asegúrese de que sus reenviadores de DNS tengan suficiente memoria o espacio en disco asignado al caché para evitar que se llene.

La cantidad de memoria que se debe dedicar al almacenamiento en caché de DNS varía mucho, desde megabytes hasta gigabytes, según la cantidad de solicitudes de DNS que se originan en los puntos finales de su red.

=== "BIND"
    Vincula cachés en la memoria de forma predeterminada, por lo que la única limitación es agotar la memoria disponible en el sistema.

     Para verificar el tamaño del caché actual, puede volcar el caché en un archivo local y luego examinar el tamaño del archivo, que será aproximadamente la cantidad de memoria que utiliza el caché:

    ```
    rndc dumpdb -all
    ```

    ```
    ls -alh /var/bind/
    ```
=== "dnsdist"
    El almacenamiento en caché está deshabilitado de forma predeterminada, pero [se puede habilitar para el almacenamiento en memoria] (https://dnsdist.org/guides/cache.html).
=== "Unbound"
    El tamaño de caché asignado está determinado por las opciones msg-cache-size y rrset-cache-size en el [archivo unbound.conf] (https://www.nlnetlabs.nl/documentation/unbound/unbound.conf/).

     Puede verificar la cantidad de memoria que su caché está usando actualmente para compararla con el tamaño de caché que asignó en unbound.conf usando el [comando unbound-control](https://www.nlnetlabs.nl/documentation/unbound/unbound -control/) para ver las estadísticas de los valores mem.cache.rrset y mem.cache.message.

=== "Knot Resolver"
    Knot Resolver almacena en caché en el disco de forma predeterminada, pero se puede configurar para usar memoria/tmpfs, backends y compartir caché entre instancias. Knot Resolver tiene [excelente documentación sobre todo lo relacionado con el almacenamiento en caché] (https://knot-resolver.readthedocs.io/en/stable/daemon-bindings-cache.html).
=== "Windows DNS Server"
El almacenamiento en caché en memoria se puede configurar utilizando el subprograma cmd `Set-DnsServerCache`.

     El uso de la memoria se puede verificar usando el subprograma cmd `Get-DnsServerStatistics`.
	 
### Utilice las direcciones IP Quad9 primaria y secundaria

Configurar la IP primaria *y* secundaria de su servicio Quad9 deseado naturalmente ayuda a equilibrar la carga de las consultas DNS en la infraestructura Quad9.

### Usar IPv6

Si su red es compatible con IPv6, configure también las direcciones IPv6 primarias y secundarias de su servicio Quad9 deseado en sus reenviadores DNS, lo que naturalmente ayuda a equilibrar la carga de las consultas DNS en la infraestructura Quad9.

Si IPv6 no está en uso, Quad9 le recomienda encarecidamente que investigue cómo habilitarlo en su red. Las rutas de ruta IPv6 suelen ser más rápidas en comparación con las rutas de IPv4, lo que genera una mayor probabilidad de éxito a velocidades más rápidas y con mejor redundancia.

### Direcciones IP separadas para cada reenviador DNS

Idealmente, cada reenviador de DNS debería enviar y recibir consultas de DNS a Quad9 utilizando diferentes direcciones públicas IPv4 e IPv6, incluso si las direcciones están dentro de la misma subred.

### Deshabilitar la validación DNSSEC

Dado que Quad9 ya realiza la validación de DNSSEC, la habilitación de DNSSEC en el reenviador provocará una duplicación del proceso de DNSSEC, lo que reducirá significativamente el rendimiento y potencialmente provocará respuestas FALSAS y falsas.

=== "dnsdist"
    Agregue esto en `dnsdist.conf` *arriba* de la asignación de su grupo.
    ```
    if noDNSSECOnNOSEC then
      addAction(NetmaskGroupRule(nmgNOSEC, false), SetDisableValidationAction(), { name="R_NO_DS" })
    end
    ```
=== "Knot Resolver"
    Agregue esto al archivo `kresd.conf` y vuelva a cargar/reiniciar el servicio `kresd`.
    ```
    -- turns off DNSSEC validation
    trust_anchors.remove('.')
    ```
=== "PowerDNS Recursor"
    En `recursor.conf`, deshabilite `dnssec` y vuelva a cargar/reiniciar `pdns-recursor`.
    ```
    dnssec=off
    ```
=== "Unbound"
    Comente estas líneas en `unbound.conf` y vuelva a cargar/reiniciar sin enlazar.
    ```
    trust-anchor-file:
    auto-trust-anchor-file:
    trust-anchor:
    trusted-keys-file:
    ```
### Deshabilitar la minimización de QNAME

La minimización de QNAME es una función de privacidad diseñada para usarse cuando se opera una solución recursiva (Quad9), pero no proporciona ninguna mejora de la privacidad y reduce significativamente el rendimiento. [¿Qué es la minimización de QNAME?](https://www.isc.org/blogs/qname-minimization-and-privacy/)
=== "BIND"
    En la sección ```options {``` del archivo nombrado.conf, agregue la siguiente línea y vuelva a cargar/reiniciar nombrado/bind9.
     ```
    qname-minimization disabled;
    ```
=== "dnsdist"
    La minimización de QNAME no es compatible con dnsdist. Nada que hacer aquí.
=== "Unbound"
    Agregue esto en `unbound.conf` y vuelva a cargar/reiniciar sin enlazar.
    ```
    qname-minimisation: no
    ```
=== "Knot Resolver"
    En el archivo `kresd.conf`, agregue una política para deshabilitar la minimización de QNAME y reinicie/recargue el servicio `kresd`.
    ```
    policy.add(policy.all(policy.FLAGS('NO_MINIMIZE')))
    ```

¿Preguntas? ¿Asuntos? ¡Contáctenos!

[Obtenga soporte](https://quad9.net/es/support/contact){ .md-button .md-button--primary }
