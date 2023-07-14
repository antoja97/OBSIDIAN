![[Pasted image 20230713124951.png]]

Infraestructura para el almacenaje y consulta de datos basada en Hadoop, la cual proporciona escalabilidad masiva y con capacidades de tolerancia a fallos, para procesamiento y almacenamiento de datos.

Proporciona lenguaje llamado HiveQL (HQL), basado en SQL-92, cuyas consultas se traducen a trabajos MapReduce que se ejecutan en Hadoop.

## ¿Qué no es Hive?

- No es gestor de BBDD relacionales
- Tiene latencia muy alta
- Para conjunto de datos pequeños su rendimiento no es comparable al de sistemas tradicionales (Oracle, MySQL, etc)
- No está diseñado para procesamiento de datos al vuelo ni ofrece consultas en tiempo real


### Tipos de datos

- Numéricos
![[Pasted image 20230713125438.png]]

- Fecha y hora
![[Pasted image 20230713125503.png]]
- Caracteres
![[Pasted image 20230713125522.png]]
- Otros
![[Pasted image 20230713125535.png]]
- Complejos
![[Pasted image 20230713125608.png]]


## Bases de datos

![[Pasted image 20230713125846.png]]
![[Pasted image 20230713125854.png]]
![[Pasted image 20230713125902.png]]
![[Pasted image 20230713125915.png]]
![[Pasted image 20230713125923.png]]
![[Pasted image 20230713125933.png]]
![[Pasted image 20230713125943.png]]
![[Pasted image 20230713125956.png]]
![[Pasted image 20230713130008.png]]
![[Pasted image 20230713130028.png]]
![[Pasted image 20230713130041.png]]
![[Pasted image 20230713130054.png]]
![[Pasted image 20230713130105.png]]
![[Pasted image 20230713130132.png]]
![[Pasted image 20230713130144.png]]
![[Pasted image 20230713130254.png]]
![[Pasted image 20230713130304.png]]
*Tablas Externas*
![[Pasted image 20230713130453.png]]

### Exploración de tablas y particiones

![[Pasted image 20230713130537.png]]

### Modificación de tablas

![[Pasted image 20230713130615.png]]

### Carga de datos

![[Pasted image 20230713130650.png]]

### Exportación de datos

![[Pasted image 20230713130726.png]]

### Consultas varias

![[Pasted image 20230713130815.png]]
![[Pasted image 20230713130838.png]]

### LIKE Y RLIKE/REGEXP

![[Pasted image 20230713130940.png]]
![[Pasted image 20230713131017.png]]


### REGEX SerDe

En resumen, Regex SerDe es un componente en Hive que permite leer y escribir datos estructurados utilizando expresiones regulares para definir el esquema y el formato de los datos. Facilita el procesamiento de datos no estructurados o semiestructurados en Hive al extraer campos específicos de una cadena de texto utilizando patrones de coincidencia de expresiones regulares.

![[Pasted image 20230713131144.png]]
![[Pasted image 20230713131430.png]]
![[Pasted image 20230713131459.png]]


### Hive:Optimización: Sort By

![[Pasted image 20230713131629.png]]


### Distribute by con Sort by

- DISTRIBUTE BY: Controla como la salida del map se divide entre los reducers, donde Hive usa esta característica internamente cuando convierte las consultas a trabajos MapReduce.
	*NOTA* * No es importante preocuparse por esto, a menos que se use Hive Streaming o algunas UDAFs (User Define Aggregation Function)

- DISTRIBUTE BY...SORT BY: asegura que las filas que tengan el mismo valor en cierto campo vayan al mismo reducer.  

- CLUSTER BY campo = DISTRIBUTE BY campo SORT BY campo ASC

### Casting

![[Pasted image 20230713132532.png]]

### UNION ALL

![[Pasted image 20230713132552.png]]

### VIEW

![[Pasted image 20230713132632.png]]


## TIPOS COMPLEJOS EN HIVE: EJEMPLOS

#Ejemplo1

![[Pasted image 20230713132727.png]]
![[Pasted image 20230713132830.png]]
En la siguiente imagen lo que vemos es lo que haríamos para crear la tabla como estas
![[Pasted image 20230713133110.png]]

Otra manera sería hacerlo con clave valor que es las 2 siguientes imágenes que veremos

![[Pasted image 20230713133221.png]]

Esta  vez usando tipo STRUCT

![[Pasted image 20230713133351.png]]
![[Pasted image 20230713133418.png]]


#### Tipo complejo: EXPLODE

La función EXPLODE en Hive se utiliza para descomponer una columna de tipo ARRAY en filas individuales.
Esto es útil cuando tienes una tabla en Hive con una columna de tipo ARRAY y deseas consultar o analizar los elementos individuales del arreglo de forma separada.


![[Pasted image 20230713133648.png]]


### Análisis de Sentimiento

Es la aplicación de Text Analytics:
	- Clasificación y mesura de opiniones
	- Frecuentemente usado en análisis de RRSS

Hive dispone de funciones para ayudarnos en este tipo de análisis

![[Pasted image 20230713133958.png]]
![[Pasted image 20230713134023.png]]

#### Análisis con n-grams

Un n-grama es una combinación de "n" palabras y se suele utilizar para **sugerir** correción de palabras cuando hacemos búsquedas, **encontrar** las palabras más importantes en los textos e **identificar** trending topics.

Esta función requiere tres parámetros:
- Array de strings
- Número de palabras en el n-grama
- Número de resultados deseados (top-N, basado en frecuencia)

La salida es un array de Structs con dos atributos
- *Ngram*: el propio n-gram (un array de palabras)
- *Estfrecuency*: la frecuencia estimada a la que este n-gram aparece

![[Pasted image 20230713134635.png]]

![[Pasted image 20230713140315.png]]

## Optimización

Hive ejecuta internamente Map Reduce y para optimizar las queries, hay que comprender como son procesadas.
![[Pasted image 20230713140444.png]]

#### *Optimización: Plan de Ejecución*

Un **job** consiste en dos fases **Map & Reduce** .
		La salida del map es la entrada del reduce.      ![[Pasted image 20230713140735.png]]
Map siempre se ejecuta primero y reduce es opcional.

![[Pasted image 20230713140833.png]]
![[Pasted image 20230713140853.png]]

##### Stage 1
Se trata de un job Map Reduce:
	- Fase Map : Lee tabla customers y selecciona zipcode y cust_id
	- Fase Reduce: Group by zipcode
![[Pasted image 20230713141103.png]]

##### Stage 0
![[Pasted image 20230713141127.png]]

##### Stage 3 y 2
![[Pasted image 20230713141220.png]]

### Optimización: Bucketing

El **partitioning** es una técnica de optimización basada en dividir los datos de una tabla en función del valor de sus columnas, en función del uso que le vayamos a dar.

El **bucketing** es otra forma de subdividir datos para ganar eficiencia:
- Calcula un código Hash para los valores insertados en la columna "bucket"
- Divide los datos en base a esa columna
- El Hash es usado para asignar nuevos valores al bucket correspondiente
 ![[Pasted image 20230713141505.png]]

En **bucketing** el número de particiones es fija, en partitioning no.
En **partitioning** todas las filas de la partición tienen la misma key.

*El objetivo del **bucket** es distribuir filas a lo largo de un número predefinido de buckets*
![[Pasted image 20230713141700.png]]
![[Pasted image 20230713141746.png]]
![[Pasted image 20230713141830.png]]

### *Optimización: Indexado*

Hive también soporta el indexado, el cual es parecido al de las RDBMS pero mucho más limitado.
Mejora el performance de algunas queries a costa de consumir más espacio en disco y CPU.
![[Pasted image 20230713142012.png]]
![[Pasted image 20230713142230.png]]

## Ventanas

Se utilizan para realizar funciones de agregación a una partición o subconjunto de filas, cuales ofrecen muchas más posibilidades que las funciones de agregación típicas.
Normalmente se utiliza el **GROUP BY**.
![[Pasted image 20230713142541.png]]

![[Pasted image 20230713142716.png]]

##### Funciones de ventana

- LEAD : Se usa para acceder a filas posteriores a la actual
- LAG : Se usa para acceder a las filas anteriores a la actual
- Ambas necesitan las cláusulas ORDER BY y PARTITION BY
![[Pasted image 20230713142847.png]]
![[Pasted image 20230713143242.png]]
![[Pasted image 20230713143340.png]]
![[Pasted image 20230713143357.png]]
![[Pasted image 20230713143433.png]]

