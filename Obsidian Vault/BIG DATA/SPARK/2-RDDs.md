
Los RDDs (Resilient Distributed Dataset) es una simple Resiliente e Inmutable colección Distribuida de objetos.

- Resiliente (tolerante a fallos): Podemos recuperar los datos en memoria si se pierden
- Inmutable: No podemos realizar modificaciones sobre un mismo RDD, ya que si queremos modificar tendremos que crear uno nuevo.
- Distribuido: Cada RDD es dividido en múltiples particiones automáticamente, pudiendo ser ejecutado en diferentes nodos del clúster.
- Dataset: Conjunto de datos, ya sean de fuentes externas o en memoria


El **Spark Context** es la manera que tenemos de comunicarnos con el clúster.

El metodo ***Parallelize*** convierte una Scala Collection local en un RDD
![[Pasted image 20230717112232.png]]

El metodo ***textFile*** lee un fichero de texto desde HDFS o Local y lo transforma en un RDD tipo String
![[Pasted image 20230717112321.png]]

Las **Transformaciones son perezosas (lazy)** ya que no se procesa hasta que se ejecute alguna acción sobre ellas, mientras que las acciones no son perezosas y el resultado es inmediatamente computado.

![[Pasted image 20230717112810.png]]


### Transformaciones

Son LAZY EVALUATION

![[Pasted image 20230717112923.png]]

Las más usadas son:
- map () : genera un nuevo RDD aplicando alguna función sobre cada línea del RDD
- filter () : Toma función y aplica a los elementos del RDD que cumplen el filtro (un WHERE de SQL)
![[Pasted image 20230717113357.png]]

- flatMap(): se itera sobre cada elemento 
 **La diferencia es que Map lo guarda en corchetes cada palabra desglosada y flatMap lo pone todo sin corchetes** .

### Acciones

La más típica es reduce()
![[Pasted image 20230717114606.png]]

- collect() para que nos devuelva o veamos lo que tenemos
- saveAsSquenceFile() para datasets muy grandes
- count()
- take(n) devuelve array de elementos
- saveAsTextFile(file) guarda el RDD a un fichero de texto


### Listado de transformaciones

![[Pasted image 20230717115023.png]]
![[Pasted image 20230717115043.png]]

### Listado de acciones

![[Pasted image 20230717115110.png]]
![[Pasted image 20230717115124.png]]


