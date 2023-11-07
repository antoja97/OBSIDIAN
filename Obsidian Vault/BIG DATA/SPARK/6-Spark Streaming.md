
No funciona totalmente en tiempo real, si no que simula el tiempo real dividiendo los datos que llegan en tiempo real en diferentes RDDs, de forma que se mezcla pa programación en lotes de Spark(BATCH) con la obtencións de datos en tiempo real.

Así como en Spark están los RDDs, en Spark Streaming tenemos los DStreams (discrtezied streams). Un DStream se compone de RDDs.

Existe un mecanismo llamado **checkpoint** que hace una copia segura de los datos cada cierto tiempo (parametrizable) para evitar este problema, por lo que si hubiese algún fallo, podemos recalcular a partir del último **checkpoint**.

### DStreams

Secuencia de datos que llegan en un periodo de tiempo, donde internamente cada uno es representado por una secuencia de RDDs que llegan en cada paso y de ahí su nombre de *discretized*.

Pueden ser creados desde varios orígenes de datos como Flume, Kafka o HDFS.

Ofrecen dos tipos de operaciones, tales como:
- *Transformations*, que generan otro DStream de uno existente.
- *Output Operations*, que escriben datos a sistemas externos. Similares a las acciones en RDDs


![[Pasted image 20230719115052.png]]
![[Pasted image 20230719115111.png]]
![[Pasted image 20230719115206.png]]
![[Pasted image 20230719115218.png]]
![[Pasted image 20230719115351.png]]

#### Transformaciones

Tenemos dos tipos de transformaciones de RDDs que se pueden usar con DStreams:
- Sin estado (stateless): donde el procesamiento de cada BATCH o RDD no depende de los anteriores.
- Con estado (stateful): donde el procesamiento de cada BATCH o RDD SÍ depende de los anteriores.

![[Pasted image 20230719115808.png]]
![[Pasted image 20230719115838.png]]


###### Operaciones de salida del DStream

![[Pasted image 20230719115909.png]]


#### **IMPORTANTE**

![[Pasted image 20230719120034.png]]


### Operaciones STATEFUL

![[Pasted image 20230719120156.png]]
* EJEMPLO

![[Pasted image 20230719120231.png]]
![[Pasted image 20230719120253.png]]
![[Pasted image 20230719120305.png]]
![[Pasted image 20230719120343.png]]
Lo que hace es ir sumando en las Total Requests
En esta img siguiente se ve muy claro
![[Pasted image 20230719120503.png]]
![[Pasted image 20230719120520.png]]


## Checkpoints

Los puntos de control son los mecanismo que tienen que ser utilizados para conseguir tolerancia a fallos en Spark Streaming.
Permiten a Spark guardar datos, periódicamente, sobre la aplicación en un sistema de almacenamiento (HDFS, Amazon S3...) para usar en caso de recuperación.

Sirve para dos propósitos:
- Spark Streaming puede recomputar el estado usando el linaje de transformaciones, pero los puntos de control establecen como de atrás tenemos que ir en dicho tráfico.
- Si el driver de una aplicación Spark falla podemos lanzarlo de nuevo y decirle que se recupere desde este punto de control.

***SPARK NO PERMITE EL USO DE OPERACIONES STATEFUL SIN CHECKPOINTING ACTIVADO***


### Windowed operations

Combinan resultados de múltiples batches.

Estas operaciones necesitan dos parámetros:
- **Window Duration**: determina cuantos batches previos hay que considerar --> p.e si tuvieramos un DStream con batches cada 10 segundos y quisiéramos crear un sliding window de 30 segundos (o 3 batches), parametrizaríamos la variable windowDuration a 30 segundos.
- **Sliding Duration**: controla como de frecuentemente el nuevo DSstream computa resultados --> p.e si tuviéramos un intervalo batch de 10 segundos y quisiéramos computar nuestra ventana solo el segundo de cada dos batch, estableceríamos el valor de sliding itnerval a 20 segundos. ***AMBOS DEBEN SER MÚLTIPLOS DE LA DURACIÓN DEL BATCH DEL STREAMINGCONTEXT***

![[Pasted image 20230719121400.png]]
![[Pasted image 20230719121415.png]]
![[Pasted image 20230719121424.png]]
![[Pasted image 20230719121442.png]]
![[Pasted image 20230719121452.png]]


#### Ejemplo:

![[Pasted image 20230719121534.png]]


### Consideraciones

![[Pasted image 20230719121610.png]]
![[Pasted image 20230719121634.png]]
![[Pasted image 20230719121650.png]]
