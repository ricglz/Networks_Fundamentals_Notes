## Arte
- Piet Mondrian, Composición con Rojo y Azul, Museo de Arte de Nueva York (MOMA)
- Civilización Zapoteca, Edificio de la cultura zapoteca, Mitla Oaxaca
- Civilización Maya, Ruinas de Uxmal, Yucatán
- Civilización Azteca, La piedra del Sol o Calendario Azteca, Museo de Antropología
- Juan Soriano, La Paloma, Museo de Arte Contemporáneo (MARCO) de Monterrey, N.L.

## Nivel transporte

- Los roles del nivel transporte son
  - Establecer sesiones de comunicación entre dos aplicaciones y mover datos entre ellas
  - Una conversación es el conjunto de datos que fluye entre una aplicación fuente y destino
  - Este nivel se encarga de segmentar los mensajes si fuese necesario, así como encapsularlos
  - El nivel transporte se encarga de asignarle a cada aplicación un número de puerto, para identificar la aplicación
  - También se encarga de manejar la confiabilidad de la conversación
- Los 2 protocolos de nivel transporte más conocidos son TCP y UDP

### TCP
- Maneja 3 operaciones básicas de confiabilidad
  1. Tracking
  2. Acknowledge
  3. Unacknowledge
- Es usado para casos donde es importante que la información no se pierda o se distorcione
- Su RFC es el **793**
- Header TCP
  - Mantiene un tracking del estado en la sesión
  - Registra cuál se ha mandado y cuáles han sido acknowledge
  - El header TCP varía, pero comúnmente es de 20 bytes
- El Header TCP se compone de
  - Source y Destination port (**2 bytes** cada uno), los cuales se usan para identificar la aplicación. **Note** Es el puerto más pequeño el que lo indica
  - Sequence number (**4 bytes**), se usa para resamblar los segmentos
  - Acknowledge number (**4 bytes**) indica que los datos han sido recibidos
  - Header lenght (**2 bytes**) indica la longitud del header. **Note** Se calcula tomando el primer nibble y multiplicándolo por 4
  - Reserved (**3 nibbles**) reservado para uso future.
  - Control bits (**3 nibbles**) son flags. **Note** normalmente usadas para saber el estado acknowledge actual.
  - Window size (**2 bytes**) indica el número de bytes que pueden ser aceptados a la vez.
  - Checksum (**2 bytes**)
  - Urgent (**2 bytes**)
- Establecimiento de la conexión TCP
  1. El cliente inicia un **requerimiento** una sesión de comunicación cliente-servidor. Usa la bandera **SYN**
  2. El servidor reconoce la sesión y requiere una sesión de comunicación de servidor-cliente. Usa las banderas **SYN, ACK**
  3. El cliente que inicia envía un mensaje con una señal de bandera de **ACK**
- El envío-recepción de datos de la conexión TCP
  1. El cliente envía datos usualmente de un protocolo de nivel superior, como HTTP. A lo que el server responde que recibió dicha petición.
  2. Se envían y reciben datos
  3. El servidor responde que ya terminó con el 200 OK de HTTP, a lo que el cliente le responde con ACK.
- Finalización de la conexión TCP
  1. El cliente avisa que termina la conexión, enviando una bandera de **FIN**.
  2. El servidor responde con las banderas de **ACK, FIN**
  3. El cliente reconoce el **ACK**
- TCP es un protocolo **Full Duplex** donde cada conexión representa 2 sesiones de un camino cada una.
- Aplicaciones que usan TCP HTTP, HTPPS, FTP, SMTP, Telnet

### UDP
- Es un protocolo que entrega segmentos con poco overhead, presenta **best-effort delivery** y **no es confiable**
- Es usado para casos donde no es importante la perdida de información.
- Su RFC es el **768**
- Su Header siempre es de 8 bytes y contiene
  - Source y Destination port (**2 bytes** cada uno), los cuales se usan para identificar la aplicación. **Note** Es el puerto más pequeño el que lo indica
  - Length (**2 bytes**)
  - Checksum (**2 bytes**)
- UDP no es orientado a conexión y no requiere procesos extra para garantizar la confiabilidad.
- Aplicaciones que usan UDP: DHCP, DNS, SNMP, TFTP, QUIC, VoIP, IPTV

### Otros
- Un socket es una combinación de la dirección IP que se encuentra en nivel 3 y el puerto de nivel 4.
- Se usa para identificar el servidor y el servicio requerido por el cliente
- La IANA es la responsable de asignar los estándares de direcciones, protocolos y números de puerto.

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
