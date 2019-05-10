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
  - Source y Destination port (**2 bytes** cada uno), los cuales se usan para identificar la aplicación. **Nota: El puerto más pequeño es el que lo indica**
  - Sequence number (**4 bytes**), se usa para resamblar los segmentos
  - Acknowledge number (**4 bytes**) indica que los datos han sido recibidos
  - Header lenght (**2 bytes**) indica la longitud del header. **Nota Se calcula tomando el primer nibble y multiplicándolo por 4**
  - Reserved (**3 nibbles**) reservado para uso future.
  - Control bits (**3 nibbles**) son flags. **Nota normalmente usadas para saber el estado acknowledge actual.**
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