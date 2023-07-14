
Encontramos con HADOOP COMMON, YARN, HADOOP DISTRIBUTED FILE SYSTEM (HDFS) Y YARN

### HDFS

Writen in Java for Hadoop framework.

HADOOP 1.0 (MapReduce and HDFS)
HADOOP 2.0 (MapReduce, Others, YARN and HDFS)

YARN mejora el poder de un cluster Hadoop, siendo compatible con MapReduce, gran capacidad y escalabilidad. 


#### HADOOP ZOO

Oozie (Workflow) , Pig (Scripting), Mahout (Machine Learning), R connectors (Statistics) and Hive (SQL Query).

![[Pasted image 20230711091840.png]]


#### APACHE SQOOP

Herramienta diseñada para una transferencia eficiente entre Apache Hadoop y base de datos relacionales.

#### PIG

Alto nivel de programación en MapReduce, usado para problemas de análisis de datos como data flows y originalmente creado por Yahoo.

#### HIVE

Software de data warehouse que facilita las queries y manejar grandes datasets en memorias distribuidas.

#### OOZIE

Workflow systema para manejar los trabajos de Apache Hadoop, el cual ayuda a MapReduce, Pig, Apache Hive y Sqoop.

#### ZOOKEPER

Proporciona servicios de operación a un cluster Hadoop, centrado en el mantenimiento, configuration, nombres y sincronización.


#### FLUME

Distribuido, de confianza y para coleccionar eficientemente, agregar y mover grandes cantidades de registros.


![[Pasted image 20230711092906.png]]


#### IMPALA 
Se usa para procesar SQL queries en data almacenada en un clsuter de Apache Hadoop.

#### SPARK

Es un motor rápido y general, para procesar grandes cantidades de datos.



## HDFS

Demonios de HDFS:
- Nodo Maestro:
	-NameNode -> Almacaenamiento y gestión de metadatos, permisos y usuarios,     bloques.
	-Secondary NameNode -> Labores de mantenimiento
	-Standby NameNode -> Para arquitecturas de alta disponibilidad, labores de mantenimiento y toma el relevo automáticamente.

- Nodos Esclavo:
	-DataNode -> Almacenan bloques de datos, no información referente al bloque en sí.,
	es el encargado de acceder a los bloques, este se almacena varias veces y gestionan las tasks de un job.


*Checkpoint del Secondary NameNode*
- Cada hora o cada 1M de transacciones, el SNN realiza checkpoint de los metadatos.



### Procedimiento de escritura en HDFS

1. Cliente conecta con el NameNode
2. El NameNode busca sus metadatos y devuelve el nombre del bloque y la lista de los DataNode.
3. El cliente conecta con el primer DataNode de la lista y empieza el envío de datos.
4. Se conecta con el segundo DataNode para realizar el envío y lo mismo con el tercero.
5. Finaliza el envío.
6. El cliente indica al NameNode donde ha realizado la escritura


### Procedimiento de lectura en HDFS

1. Cliente conecta con el NameNode
2. El NameNode devuelve una lista con los DataNode que contienen ese bloque.
3. El cliente conecta con el primer node los DataNode y comienza la lectura del bloque.


### Fiabilidad y recuperación de datos en HDFS

1.  Los DataNode envían "heartbeats" al NameNode cada 3 segundos para indicar su estado.
2. Si pasado el tiempo (por defecto 5 mins) el NameNode no recibe el heartbeat de alguno de los nodos, da por perdido ese nodo.
	- El NameNode averigua los bloques que había en el nodo perdido.
	- El NameNode busca otros DataNode donde realizar la copia de los bloques perdidos y así mantener el número de replicación. Los dataNode serán los encargados de realizar la copia de los bloques "perdidos".
3. En caso de recuperar el nodo perdido, el sistema automáticamente decidirá que bloques eliminar para mantener el número de replicación de bloques.

4. *Speculative Execution* -> Si el master detecta que un nodo esclavo está ejecutando las task más lento de lo normal, se ordena lanzar los trabajos a otro nodo esclavo y quien termine primero, entregará el resultado.

### WEB UI

A través de la web UI del NameNode seremos capaces de ver el estado de nuestro cluster:​
    
	 Espacio total del HDFS​
    
	Espacio ocupado del HDFS​
    
	Espacio disponible del HDFS​
    
	Estado de los Nodos​
    
	Navegación por el sistema de ficheros​
    
Por defecto se encuentra en el puerto 50070

### Acceso a datos a través de línea de comandos

![[Pasted image 20230712120234.png]]



## MapReduce

Se ejecuta en tres etapas:
- Fase Map
- Fase Shuffle&Sort
- Fase Reduce

Distribuye tareas a lo largo del clúster, y automáticamente las paraleliza y distribuye, siendo tolerante a fallos.

### Conceptos fundamentales

#### Mapper

Actúa sobre cada registro de entrada, cada task opera sobre un único bloque en HDFS siempre que sea posible, operando también en el nodo donde el bloque está almacenado.
*La salida del Map es un par (Clave/Valor*

#### Shuffle&Sort

Ordena por clave y agrupa  los datos intermedios de todos los mappers de una misma clave en el formato (K, [V1...Vn])

#### Reducer

Recibe la salida del S&S y realiza operaciones sobre ella, produciendo la salida final.

![[Pasted image 20230713085719.png]]


#EJEMPLO WORDCOUNT BIEN EXPLICADO

![[Pasted image 20230713090401.png]]


#### ¿Por qué WordCount?

Contar palabras es uno de los desafíos más típicos cuando se trabaja sobre enormes cantidades de datos.

La agregación de valores es muy usada en análisis de datos (max, min, suma, contador, etc.)

![[Pasted image 20230713090705.png]]


### Demonios de MapReduce V1

- Jobtracker : 1 por clúster, corre en nodo/s maestro activo, gestiona los jobs MR y distribuye Tasks entre TaskTrackers

- TaskTracker : 1 por nodo esclavo, y ejecuta y monitorea cada task map y reduce

### Demonios de MapReduce V2-Yarn

Su objetivo es descargar de trabajo al JobTracker, quien se encarga de todo en la V1.
Podríamos decir que es contratar encargados que se encarguen de trabajos específicos para que el jefe se pueda encargar de otras cosas de otro índole o mayor nivel.

Sus demonios son:

- Resource Manager : 1 por clúster, arranca el ApplicationMasters y dota de recursos (CPU, RAM) a los nodos esclavos.

- ApplicationMasters : 1 por Job, pide recursos y gestiona cada task map, reduciendo el conjunto de nodos en los que se ejecutan las tareas asociadas al job.

- Node Manager : 1 por nodo esclavo y gestionar los recursos de cada esclavo

- Containers: Conjunto de recursos recidos por el RM tras petición

- JobHistory: 1 por clúster y almacena las métricas de los jobs y  metadatos.


#Terminología

*Job* --> Programa entero, una ejecución completa de Maps y Reduces sobre un dataset
*Task* --> Ejecución de un solo Map o Reduce sobre una porción de datos, habitualmente un bloque


### *¿La S&S puede empezar antes de que Map haya terminado?*

Los Mappers empiezan a enviar datos a los Reducers tan pronto como van acabando sus Task a través de la fase S&S, de modo que el tráfico de red se genera de forma progresiva, no al mismo tiempo.
Cierto es que los Reducers no empiezan hasta que S&S haya finalizado completamente.


#### Detalle del proceso

![[Pasted image 20230713092307.png]]


## MapReduce: Wordcount por partes

### *Driver*

![[Pasted image 20230713092528.png]]
![[Pasted image 20230713092614.png]]
![[Pasted image 20230713092712.png]]
![[Pasted image 20230713092822.png]]
![[Pasted image 20230713092900.png]]



### *Mapper*

![[Pasted image 20230713093454.png]]
![[Pasted image 20230713093111.png]]
![[Pasted image 20230713093149.png]]
![[Pasted image 20230713093416.png]]



### *Reducer*


![[Pasted image 20230713093527.png]]
![[Pasted image 20230713093603.png]]
![[Pasted image 20230713093620.png]]


# Introducción al Ecosistema Hadoop

## *Hive*

Software para interrogar, consultar y manipular datos en HDFS, pudiendo trabajar en un lenguaje similar a SQL, llamado HQL, cuya característica fundamental es que traduce *Queries HQL a MapReduce*

![[Pasted image 20230713123415.png]]


## *Pig*

Plataforma para analizar grandes datasets almacenados en HDFS, el cual tiene un lenguaje semejante a HQL pero menos que Hive, siendo su principal característica que transforma sus consultas PigLatin en MapReduce.

![[Pasted image 20230713123609.png]]

## *Sqoop*

Su principal función es traer datos datos desde BBDD relacionales a HDFS, cuya sintaxis consta de una parte de configuración + otra de SQL.

![[Pasted image 20230713123740.png]]

## *Flume*

Herramienta diseñada para importar datos en un clúster en tiempo real, pensada para orígenes de datos diferentes a BBDD relacionales (servidores web, de correo, logs de dispositivos)

![[Pasted image 20230713124009.png]]


## *Kafka*

El objetivo es proporcionar una plataforma unificada de alto rendimiento y baja latencia para manipulación en tiempo real de fuentes de datos.
Se puede ver como una cola de mensajes bajo el patrón publicación-subscripción, masivamente escalable y concebida como un registro de transacciones distribuidas.

![[Pasted image 20230713124201.png]]


## *Base de datos No-SQL*

Significa Not Only SQL y están pensadas para trabajar con datos multiestructurados, permitiendo la distribución de datos y la ejecución en paralelo. 
No garantizan completamente ACID (atomicidad, consistencia, aislamiento y durabilidad), pero si escalan muy bien horizontalmente y están pensadas para millones de columnas por billones de filas.

![[Pasted image 20230713124427.png]]


# Planificación Clúster Hadoop

![[Pasted image 20230713124621.png]]
![[Pasted image 20230713124708.png]]


