
Interfaz preparada para trabajar con datos estructurados (con schema) y semiestructurados.

Tiene tres capacidades básicas:
1. Cargar datos estructurados tipo JSON, Hive, Parquet, etc.
2. Procesar consultas relacionales
3. Tiene integración con python/java/scala.


Los DataFrames son RDDs de registros distribuídos con esquema conocido, cuyas transformaciones son conocidas como no tipadas.

Para empezar sparkSQL necesitamos SparkSession, que es un SparkContext para SparkSQL.

import org.apache.spark.sql.SparkSession


![[Pasted image 20230719091154.png]]
![[Pasted image 20230719091247.png]]
![[Pasted image 20230719091316.png]]
![[Pasted image 20230719091340.png]]
![[Pasted image 20230719091355.png]]
![[Pasted image 20230719091439.png]]
![[Pasted image 20230719091454.png]]

- Show
- printSchema()
- filter
- ![[Pasted image 20230719091657.png]]
- Joins
![[Pasted image 20230719091738.png]]
![[Pasted image 20230719091844.png]]


### DataSets
![[Pasted image 20230719092009.png]]
![[Pasted image 20230719091941.png]]
![[Pasted image 20230719092031.png]]


### ¿Cuándo usar cada uno?

![[Pasted image 20230719092119.png]]
![[Pasted image 20230719092159.png]]
![[Pasted image 20230719092226.png]]
