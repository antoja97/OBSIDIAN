
![[Pasted image 20230714125623.png]]

Es un motor de MPP: procesamiento masivo en paralelo, con latencias en milisegundos.
Corre sobre clusters Hadoop y puede ejecutar Queries sobre HDFS o Hbase.

#Características 

Ejecuta las queries directamente sobre el clúster en lugar de ejecutar un MapReduce, siendo en torno unas 5 veces más rápido que Hive o Pig.

### Comparativa con RDBMs

![[Pasted image 20230714130002.png]]

### Más características

![[Pasted image 20230714130135.png]]

##### Impala no posee tolerancia a fallos, ya que si uno falla durante la ejecución, toda la ejecución fallo, por lo que habría que volver a lanzar la query.


### Optimización

![[Pasted image 20230714130301.png]]
![[Pasted image 20230714130317.png]]
![[Pasted image 20230714130333.png]]

#ImpalavsHive

![[Pasted image 20230714130406.png]]
