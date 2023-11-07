![[Pasted image 20230716073723.png]]


Herramienta para transferir datos entre RDBMs y Hadoop.
El escenario típico será tener datos almacenados en Base de Datos Relacionales que queremos operar aprovechando la potencia de Hadoop.
	Datos de Uso general
	Datos Legacy

Por ello la *solución* es usar Sqoop para importar datos.

![[Pasted image 20230716074044.png]]


### Sqoop : de SQL a Hadoop

Es una herramienta Open Source, cuyo nombre viene de SQL to Hadoop.

Su objetivo como ya se ha comentado es la transferencia de datos entre RDBMs y Hadoop (HDFS).
Las opciones que encontramos son:
- Transferir una sola tabla
- Todas las tablas de una BBDD
- Transferir partes de una tabla. **Sqoop soporta el WHERE de SQL**

Para la importación de datos utiliza **MapReduce**:
- Permite determinar cuantos maps se pueden ejecutar a la vez
- Por defecto son 4 maps, aunque es configurable
- Da la posibilidad de paralelización y tolerancia a fallos
- Los datos son importados registro a registro


#Características

Los datos son importados a HDFS como **text files** delimitaas o SequenceFiles (Por defecto se importan como text files *separados por comas*).
Además son importados mediante MapReduce, por lo que se almacenan en formato .0

![[Pasted image 20230716074649.png]]


## + Datos importantes

##### Conectores Genéricos
![[Pasted image 20230716074819.png]]

##### Conectores a medida
Existen conectores específicos para diferentes BBDD. cuyo objetivo es proveer de una interfaz más rápida de importación y suelen ser gratis, pero no opensource.
![[Pasted image 20230716075024.png]]

##### Compatibilidad
![[Pasted image 20230716075056.png]]


## Sintaxis Básica

![[Pasted image 20230716075205.png]]

#Ejemplo

![[Pasted image 20230716075243.png]]
![[Pasted image 20230716075334.png]]

**Opciones Import**
![[Pasted image 20230716075358.png]]

##### Otras opciones
Para exportar datos desde HDFS e insertarlos en una tabla existente en una RDBMS --> sqoop export [options]

La ayuda en Sqoop --> sqoop help

Para obtener ayuda de un comando en particular --> sqoop help command


### Hive

Es posible importar datos directamente a Hive en lugar de hacerlo a HDFS
Para ello se utiliza el comando --hive-import.

En este caso Sqoop genera las siguientes acciones:
- Si la tabla hive ya existe, se puede indicar la condición **overwrite** para que sobreescriba los datos en la tabla
- Sqoop generará un script hive con la creación de la tabla si no está creada
- Sqoop generara una instrucción de carga para mover los datos importados al warehouse de hive

![[Pasted image 20230716075836.png]]

![[Pasted image 20230716075854.png]]
![[Pasted image 20230716075910.png]]



