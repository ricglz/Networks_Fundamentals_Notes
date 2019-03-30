## Nivel transporte

- Pinturas:
  - Piet Mondrian, Composición con Rojo y Azul, Museo de Arte de Nueva York (MOMA)
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
    - Source y Destination port (**2 bytes** cada uno), los cuales se usan para identificar la aplicación. _Note_ Es el puerto más pequeño el que lo indica
    - Sequence number (**4 bytes**), se usa para resamblar los segmentos
    - Acknowledge number (**4 bytes**) indica que los datos han sido recibidos
    - Header lenght (**2 bytes**) indica la longitud del header. _Note_ Se calcula tomando el primer nibble y multiplicándolo por 4
    - Reserved (**3 nibbles**) reservado para uso future.
    - Control bits (**3 nibbles**) son flags. _Note_ normalmente usadas para saber el estado acknowledge actual.
    - Window size (**2 bytes**) indica el número de bytes que pueden ser aceptados a la vez.
    - Checksum (**2 bytes**)
    - Urgent (**2 bytes**)

### UDP
  - Es un protocolo que entrega segmentos con poco overhead, presenta **best-effort delivery** y **no es confiable**
  - Es usado para casos donde no es importante la perdida de información.
  - Su RFC es el **768**
  - Su Header siempre es de 8 bytes y contiene
    - Source y Destination port (**2 bytes** cada uno), los cuales se usan para identificar la aplicación. _Note_ Es el puerto más pequeño el que lo indica
    - Length (**2 bytes**)
    - Checksum (**2 bytes**)

### Otros
  - Un socket es una combinación de la dirección IP que se encuentra en nivel 3 y el puerto de nivel 4.
  - Se usa para identificar el servidor y el servicio requerido por el cliente
  - La IANA es la responsable de asignar los estándares de direcciones, protocolos y números de puerto.
