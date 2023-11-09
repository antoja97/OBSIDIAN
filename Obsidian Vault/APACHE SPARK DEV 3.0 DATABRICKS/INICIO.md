
## 1. Cluster Architecture

Spark sigue arquitectura maestro-esclavo con un administrador de clúster (Clúster Manager), lo cual aporta escalabilidad y tolerancia a fallos.

![[Pasted image 20231107095847.png]]

## 2. Cluster Manager

Es el responsable de asignar recursos a través de la aplicación de Spark. El Spark context es capaz de conectarse a varios tipos de administradores de clúster como Mesos, Yarn o Kubernetes, a parte del administrador de clúster independiente de Spark.


## 3. Cluster

Un cluster agrupa los recursos de varias máquinas juntas, posibilitando el uso de estos en una sola máquina mediante un framework que coordina el trabajo entre nodos.

Cada cluster tiene un Driver y uno o más executors. El trabajo se divide en trabajos (jobs), los cuales se dividen en etapas (stages), y cada etapa puede tener distintas tareas (task).
La entrada a un trabajo se divide en 1 o más particiones, cuyas particiones son la unidad de trabajo de cada slot.

Entre los componentes más potentes de Spark se encuentran Spark SQL, donde en su núcleo se encuentra el optimizador Catalyst.

## 4. Driver node

Mantiene la información de estado de todos los notebooks conectados al clúster. Este también mantiene el SparkContext e interpreta los comandos que ejecuta desde un notebook o biblioteca en el clúster, y ejecuta el Apache Spark **master** que se coordina con los executors de Spark.

###### IMPORTANTE : El driver no "toca" o no utiliza en ningún momento los dataframes que se usan. El objetivo es orquestar a los ejecutores para repartir y administrar las tasks.


## 5. Daemon

Driver que inicia los executors. Son subprocesos que se ejecutan en la JVM.


## 6. Worker node

***Para ejecutar un trabajo de Spark necesitas al menos un worker node***

Databricks ejecuta un executor por nodo worker, por lo tantos, los términos executor y worker se usan indistitntamente en el contexto de la arquitectura Databricks.


### 7. Executor node

Databricks ejecuta un executor por worker node.

*Es la parte de la RAM en el nodo esclavo (nodo worker) donde se reside el bloque de datos y a tarea (task) o el codigo que se implementará. Cada aplicación de Spark tiene su propio proceso de ejecución.*

**¡OJO!  LAS TASK SE EJECUTAN EN LOS SLOTS, PERO SUS RESULTADOS SE ALMACENAN EN EL EJECUTOR***

El executor **ES** el entorno de trabajo, el cual contiene los slots que se encargan de ejecutar las tasks. 


### 8. Slots

Se tratan de los threads (hilos) que tiene disponible cada executor.
La documentación de Spark se refiere a estos threads como núcleos (cores) **NO CONFUNDIR CON LOS CORES FÍSICOS DEL CPU**

***De una manera más simple, el SLOT es como el hueco en el que poder hacer una tarea (sería como un espacio en una mesa).
En Databricks dan del tirón máquinas contando con sus hilos y los llaman también cores**


### 9. Spark Context

Conexión a un entorno de ejecución de Spark. Es un punto de entrada para un SparkJob.

Se usa para crear RDDs, acumuladores, variables broadcast, acceder a servicios de Spark y correr trabajos.

**RESUMIDO: Es un cliente del entorno de ejecución de Spark y actúa como el master de su Spark**.


### 10. Spark conf

Permite configurar algunas de las propiedades comunes (por ejemplo, la URL maestra y el nombre de la aplicación), así como pares clave-valor arbitrarias a través del método set().

Ejemplo: 

![[Pasted image 20231108160623.png]]


# Spark execution hierarchy












