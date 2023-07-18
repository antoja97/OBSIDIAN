![[Pasted image 20230717092352.png]]

Hoy en día existen multitud de fuentes de datos, donde sabemos que hay dos maneras de catalogar los datos en función del tiempo de espera hasta obtener resultados.
- Batch (Lotes)
- Real Time

## Definición y conceptos básicos

Apache Flume es un sistema distribuido, confiable y preparado para recopilar, agregar y mover de forma eficiente grandes cantidades de diversas fuentes a un almacén de datos centralizado.

- Tiene arquitectura sencilla y flexible basada en flujos de datos en streaming
- Robusto y tolerante a fallos con múltiples mecanismo de configuración.

**Flume** significa "*Canal Artificial*"
**Log** se peude traducir como "*Tronco*"


### Componentes

- **Event** : Es la unidad de dato que se va propagando a través de la arquitectura.
- **Source**: Origen de los datos
- **Sink**: Destino de los datos
- **Channel**: Buffer de almacenamiento intermedio que conecta el source con el sink

![[Pasted image 20230717093005.png]]

### Setup + Ejemplo

![[Pasted image 20230717093129.png]]
![[Pasted image 20230717093146.png]]


### Opciones de configuración

**Un único flujo/agente**
- Es el ejemplo de arriba
- Definimos el agente dentro de "a1"
- Conectamos source y sink a través del channel
- Un source puede estar conectado a varios channels, pero un sink solo puede estar conecta a un channel.

**Múltiples agentes**
- Se necesita que el sink del agente previo y el source del actual tienen que ser tipo AVRO (sistema de serialización de datos), con el sink apuntando al hostname y puerto del source.

![[Pasted image 20230717093443.png]]

- Un caso de este tipo de configuración es la de múltiples webs enviando logs a un sistema de almacenamiento como HDFS

![[Pasted image 20230717093549.png]]

**Múltiples flows**

La idea es multiplexar los eventos a uno o más destinarios en función de una serie de condiciones indicadas en el fichero de configuración, existiendo dos opciones:
- Replica: donde todos los eventos se mandan sobre todos los canales
- Multiplexación : donde los eventos se mandan sobre ciertos canales en función de las propiedades de selección

![[Pasted image 20230717093818.png]]



## Detalle de configuración

![[Pasted image 20230717093956.png]]
![[Pasted image 20230717094015.png]]
![[Pasted image 20230717094049.png]]
![[Pasted image 20230717094106.png]]

## Sources

Existen numerosos tipos de fuentes de datos soportados por Flume, los cuales se pueden parametrizar y desde el punto de vista funcional encontramos dos tipos:

- **EvenDriverSource** : Son activos y controlan cómo y cuando los eventos son añadidos al channel. Responden al comportamiento *push*. El ejemplo más claro es el Avro source. Cuando recibe un *RPC* (Remote Procedure Call) con uno o más eventos, inmediatamente los añade al channel.

- **PollableSource**: Son pasivos, no hay forma de saber cuando llega un nuevo dato que será enviado a través del flow, por lo que **Flume** tiene que "tirar de ellos:*pull*" cada cierto tiempo. Además son fáciles de configurar pero proveen menos control.

##### Predefinidos

![[Pasted image 20230717094709.png]]
![[Pasted image 20230717094734.png]]


## Sinks

Se encargan de extrar evento de un channel y almacenarlos en un sistema externo o enviarlos al siguiente agente del flow

![[Pasted image 20230717094809.png]]

#### Predefinidos

![[Pasted image 20230717094857.png]]


## Channels predefinidos

![[Pasted image 20230717094935.png]]


## Interceptores

Flume permite modificar eventos en caliente mediante interceptores, los cuales actúan como si fuera una pequeña **ETL** con una serie de funciones predefinidas.

Implementan la inferfaz org.apache.flume.interceptor.interceptor

Si hay varios, se ejecutan en el orden que se hayan definido se irán pasando de uno a otro de manera encadenada.

#### Predefinidos

![[Pasted image 20230717095133.png]]


