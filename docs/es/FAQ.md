## ¿Cómo confirmo que estoy usando Quad9?

La prueba más sencilla es abrir [on.quad9.net](https://on.quad9.net) en el navegador de su elección.

## Prueba de protocolo: confirme en qué protocolo Quad9 recibió su consulta

Confirme qué protocolo se utiliza cuando Quad9 recibe sus consultas de DNS. Esto es particularmente relevante después de configurar el cifrado DNS, como DNS sobre TLS o DNS sobre HTTPS, en el sistema operativo, enrutador o reenviador de DNS.

Ejecute el siguiente comando y consulte las posibles respuestas a continuación:

=== "Windows (PowerShell/Terminal)"

    `Resolve-DnsName -Type txt proto.on.quad9.net.`
=== "MacOS/Linux/Unix (Terminal)"

    `dig +short txt proto.on.quad9.net.`

Posibles respuestas:

* do53-udp (53/UDP - Plaintext)
* do53-tcp (53/TCP - Plaintext)
* doh (443/TCP - DNS over HTTPS)
* dot (853/TCP - DNS over TLS)
* dnscrypt-udp (UDP - DNSCrypt)
* dnscrypt-tcp (TCP - DNSCrypt)

Si no recibe una respuesta (NXDOMAIN), entonces Quad9 no se utilizó para realizar esta consulta de DNS.

## Identificando un bloque Quad9

La forma más rápida de ver si un dominio está bloqueado en Quad9 es utilizando nuestro [Probador de dominios bloqueados] (https://quad9.net/es/result).

Cuando Quad9 bloquea un dominio, la respuesta es "NXDOMAIN". `NXDOMAIN` también se devuelve cuando un dominio no existe. Para diferenciar entre dominios que no existen y dominios que están bloqueados, configuramos el valor `AUTHORITY` de manera diferente. Cuando recibe un `NXDOMAIN` con `AUTHORITY: 0`, ese es un bloque de Quad9. Cuando recibe `NXDOMAIN` *con* `AUTHORITY: 1`, entonces ese es un dominio que no existe.

Un dominio tampoco se resolverá si falla la autenticación DNSSEC, pero eso dará como resultado el código "SERVFAIL" en lugar de "NXDOMAIN".

=== "Dominio bloqueado"

    `dig @9.9.9.9 isitblocked.org | grep "status\|AUTHORITY"`
    ```
    ;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 29193
    ;; flags: qr rd ad; QUERY: 1, ANSWER: 0, AUTHORITY: 0, ADDITIONAL: 1
    ```
=== "Dominios que no existen"

    `dig @9.9.9.9 sfaisofnadgre.odafds | grep "status\|AUTHORITY:"`
    ```
    ;; ->>HEADER<<- opcode: QUERY, status: NXDOMAIN, id: 22595
    ;; flags: qr rd ra ad; QUERY: 1, ANSWER: 0, AUTHORITY: 1, ADDITIONAL: 1
    ```
=== "Falla de DNSSEC"
    
    `dig @9.9.9.9 A brokendnssec.net +dnssec | grep status`
    ```
    ;; ->>HEADER<<- opcode: QUERY, status: SERVFAIL, id: 40999
    ```

## Detección de redirección transparente de DNS (secuestros)

Algunos ISP, con mayor frecuencia en Asia, África o el Medio Oriente, redirigirán de forma transparente las solicitudes de DNS destinadas a servicios DNS de terceros, como Quad9, a sus propios reenviadores/servidores de DNS. Esto puede ser un intento de hacer cumplir las políticas/leyes locales, o simplemente aumentar la tasa HIT de caché en sus reenviadores de DNS.

Puede detectar una redirección DNS transparente ejecutando el siguiente comando desde el símbolo del sistema o la terminal de cualquier sistema operativo. Si la respuesta es cualquier cosa excepto `resXXX.xxx.rrdns.pch.net`, entonces el DNS se está redirigiendo de forma transparente.

=== "Windows (PowerShell)"

    ```
    nslookup -q=txt -class=chaos id.server. 9.9.9.9 | Select-String "pch"
    ```

=== "MacOS/Linux/BSD (Terminal)"
    ```
    dig +short ch txt id.server. @9.9.9.9
    ```
Si el resultado no se parece al siguiente, o no hay ningún resultado, entonces el DNS se está redirigiendo de forma transparente.

=== "Windows (PowerShell)"
    ```
    Non-authoritative answer:
    "res200.vie.rrdns.pch.net"
    ```

=== "MacOS/Linux/BSD (Terminal)"
    ```
    "res860.qfra3.rrdns.pch.net"
    ```
### Mi ISP está redirigiendo DNS de forma transparente. ¿Ahora que?

Consulte nuestras Guías de configuración adjuntas con "(Encriptado)" en el título. Al utilizar DNS cifrado, no será posible la redirección de DNS transparente.

## ¿Qué es la subred del cliente EDNS (ECS)?

El servicio `9.9.9.11` de Quad9 es compatible con ECS.

La subred de cliente (ECS) de EDNS permite a Quad9 enviar una parte de su dirección IP a servidores de nombres autorizados, lo que ayuda a los principales proveedores de contenido (CDN), como Google, Microsoft, etc., a determinar con precisión su geolocalización.

ECS no tendrá ningún efecto sobre a qué ubicación de Quad9 se envían sus consultas, simplemente afecta la información que Quad9 reenvía al servidor de nombres autorizado y puede afectar la dirección IP que devuelven. Quad9 utiliza direcciones Anycast para garantizar que se le dirija a la ubicación Quad9 más cercana disponible para usted, independientemente de si utiliza o no nuestro servicio ECS.

Dado que ECS no desempeña ningún papel a la hora de determinar a dónde se envían sus consultas, no tiene ningún efecto positivo o negativo en el tiempo de ida y vuelta (ping) a Quad9.

ECS puede verse como una compensación entre la privacidad y la obtención de contenido geoespecífico. Una opción para el usuario centrado en la privacidad es dejarlo deshabilitado y habilitarlo solo si nota que un dominio específico no le entrega el contenido correcto o no se carga en absoluto.

## Proveedores de red/Pruebas de fugas de DNS

Quad9 utiliza múltiples proveedores de red en nuestra red global. Al ejecutar una prueba de fugas de DNS, se espera ver direcciones IP propiedad de los siguientes proveedores:

!!! tenga en cuenta "Herramienta de prueba de fugas de DNS recomendada"
    [dnscheck.tools](https://dnscheck.tools/)

* WoodyNet
* PCH.net
* GSL Networks
* i3D
* EdgeUno
* Equinix Metal (Packet, Packet.net, Packethost)
* Path.net (Path Network)

Estas organizaciones también figuran en la página de Patrocinadores del sitio web de Quad9: [quad9.net/about/sponsors](https://quad9.net/about/sponsors)

Si simplemente intenta determinar si está utilizando Quad9, puede visitar [on.quad9.net](https://on.quad9.net) en lugar de depender de una prueba de fuga de DNS. Sin embargo, una prueba de fuga de DNS puede ser útil para asegurarse de que está utilizando exclusivamente Quad9, lo cual es necesario para garantizar que todas sus solicitudes de DNS estén protegidas por Quad9.
