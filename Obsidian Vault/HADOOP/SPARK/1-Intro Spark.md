![[Pasted image 20230717105457.png]]



## Scala y Spark

Spark, su API principal y el Spark Shell están escritos en Scala, por lo que SPARK utiliza multitud de funciones de Scala.

Ofrece mejor rendimiento y no solo en términos de **tiempo de ejecución** , sino en términos de interactividad: : se puede ejecutar una query sobre datos en streaming y generar un nuevo streaming a partir de ellos combinable con otros datos para su posterior análisis. Por ejemplo, en webanalytics, podemos ejecutar queries contra datos que se están produciendo ahora mismo.​

Es una extensión del modelo MapReduce, cuyo objetivo es soportar más tipos de computación específicamente en streaming.


# Spark

- Para llevar a cabo toda esta computación utilizaremos Apache Spark, que no es más que un framework para programación distribuida sobre datos en paralelo.​
    
- Para ello, Spark implementa un modelo de datos  paralelos distribuidos llamado RDD: Resilient Distributed Dataset​
    
- A partir de ahora, tenemos que pensar en nuestros datos distribuidos como si fueran una única colección

**En cuanto a latencia, debemos comentar que el orden por velocidad sería Memoria, Disco y Red.**

Es mucho más rápido que Hadoop, mejorando la productividad de los analistas de datos y además en Hadoop no es fácil crear un bucle que itere sobre los datos hasta que se cumpla una condición.

![[Pasted image 20230717110125.png]]

**Spark almacena los datasets en *memoria*, mientras que Hadoop lo hace en disco**

La idea es mantener los datos inmutables y en memoria todo el tiempo. 
El resultado de esto es una mejora de hasta 100 veces en el tiempo de procesado.


###### De paralelismo al distribuido

![[Pasted image 20230717110416.png]]
![[Pasted image 20230717110434.png]]




## Introducción al análisis de datos

**Spark Core**

Contiene las funciones básicas de Spark y es el lugar donde se aloja la API que define los RDD (Resilient Distributed Dataset) , lo cual representa una colección de elementos distribuidos a través de los nodos del clúster y que pueden ser manipulados en paralelo.

**Spark SQL**

Se llamaba Shark y es el paquete a trabajar con datos estructurados de SQL o HQL, soportando varios tipos de datos como Hive, Parquet o JSON.
Permite intercalar comandos de manipulación de RDDs , permitiendo análisis potente.

**Spark Streaming**

Componente de Spark que permite procesar streams de datos en tiempo real, como por ejemplo weblogs o serverlogs mientras se van generando.


**MLlib**

Librería que contiene funcionalidades comunes de Machine Learning, como Clasificación, Regresión, Clustering, filtros colaborativos, evaluación de modelos e importación de datos.


GraphX

Librería para manipular grafos y ejecutar computación paralela sobre ellos.


![[Pasted image 20230717111104.png]]

