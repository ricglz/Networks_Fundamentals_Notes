## Nivel Red

- Este nivel permite a los dispositivos finales intercambiar datos a través de la red.
- Tiene 4 procesos básicos
  - Direccionamiento. Permite que cada terminal posee una IP única en la red.
  - Encapsulación. Encapsula una Unidad de Datos de Protocol (PDU), con la finalidad de darle información sobre el IP que tendrá.
  - Ruteo. Para llegar al destino que se encuentra en otra red, el nivel red necesita que el router al que esté conectado le permita acceder al otro router para llegar a la red. El proceso de ir de router en router se le llama hop.
  - Desencapsulación. Cuándo el paquete llega al destino, se verifica que el IP sea el del destino. Si es así se pasa al siguiente nivel (Transporte).
- Protocolos de este nivel: IPv4, IPv6, ICMP, ICMPv6

### IP

- El protocolo IP fue diseñado como un protocolo con bajo overhead.
- Proporciona las funciones necesarias para entregar un paquete.
- Es connectionless, lo que significa que **no se crea una conexión** end to end
- Es de best effort delivery
- Es independiente del medio por el cual se transmiten los datos

### Enrutamiento

- **Loopback interface** es cuando se envía paquetes a sí mismo a la dirección 127.0.0.1. Si se realiza PING a dicha dirección, se determina si está activo los protocolos TCP/IP.
- **Local host** es una dirección de un host que se encuentra en la misma red.
- **Remote host** es una dirección de un host que **no** se encuentra en la misma red.
- El enlace que tiene un router a la red local se le denomina **local gateway**
- En una tabla de ruteo se muestran las redes de la misma red y aquellas redes remotas a las que se puede accesar con hops.

### IPv4

- Sus direcciones están compuestas de 4 bytes
- Comunicación IPv4
  - Unicast: El proceso original de enviar un paquete de un host a otro.
  - Broadcast: El proceso de enviar un paquete a todos los demás en la red.
  - Multicast: El proceso de enviar un paquete a un grupo seleccionado en la red. De la 224.0.0.0 a 224.0.0.255 están reservadas para multicast en redes locales.
  - La NAT permite relacionar las IP privadas con las públicas.
- Existe una dirección especial llamda APIPA que cubre 169.254.0.0/16 (169.254.0.1 a 169.254.255.254)

### IPv6

- Se creo por consecuencia del agotamiento de direcciones de IPv4. Estas nuevas direcciones IPv6 están formadas de 16 bytes cada una.
- En la actualidad esto está tomando aún mayor relevancia debido a la implementación del Internet of Things (IoT), la cual requiere de aún más direcciones para una mayor cantidad de dispositivos.
- Aunque no es oficial comúnmente se usa la notación por hextetos. Es decir que se interpretan 2 bytes de forma hexadecimal y estos se van juntando con un ":" de intermedio.
- Para hacer la notación de hextetos compresa se deben realizar los siguientes 2 pasos.
  1. Omitir los 0s que se tengan a la izquierda del hexteto.
  2. Omitir todos los hextetos que sean únicamente 0s.
- Ejemplos
  - "0001:0002:0003:0004" simplificado completamente es: "1:2:3:4"
  - "0001:0000:0000:0002" simplificado completamente es: "1::2"
- La longitud de prefijo fijo en IPv6 se usa para representar la porción de la dirección. Tiene un rango de 0-128
- Direcciones IPv6 unicast
  * Son globales y enrutables, siendo equivalentes a las direcciones públicas de IPv4.
  * Tienen un prefijo de ruteo, cuyo valor más común es /48
- Hay dos formas en las que un dispositivo puede tener una dirección IPv6 dinámica
  * Mediante **SLAAC** que significa Stateless Address Autoconfiguration
  * O mediante **DHCPv6**
- Hay varias formas de crear coexistencia entre IPv4 e IPv6
  * **Dual stack**, el router permite tanto IPv4 como IPv6
  * **Tunneling**, el paquete IPv6 se encapsula en un paquete IPv4
  * **Translation**, el cual permite hacer una conversión equivalente al NAT de IPv4 usando un mecanismo llamado NAT64

### ICMP

- En caso de paquetes con error se envían de regreso paquetes mediante el protocolo ICMP encapsulado en IP.
- Sólo hace un ECHO.
- ICMP existe tanto para la versión IPv4 como IPv6.
- Su RFC es el 792.
- Es usado para herramientas de **ping** y **traceroute**

### ARP

- Significa **Address Resolution Protocol**
- Se usa para obtener la dirección MAC de una dirección IP.

### Subnetting (subneteo)

- El subneteo reduce el tráfico en la red
- Permite implementar políticas de seguridad
- El subneteo se hace incrementando  el tamaño de la máscara. Con el objetivo que estos bits extras sean usados para crear las subredes en potencias de 2.
- Ejemplo:

**En este caso lo que se hace es usar un bit más de los 24 comúnes y con ese bit más puedes tener más subredes. Sin embargo pierdes parte de los hosts.**

| Tamaño máscara| # subredes    | #hosts  |
| :-----------: |:-------------:| :------:|
| /25           | 2             | 126     |
| /26           | 4             | 62      |
| /27           | 8             | 30      |