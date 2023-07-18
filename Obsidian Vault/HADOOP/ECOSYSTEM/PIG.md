![[Pasted image 20230715181734.png]]


#ConceptosBásicos

*Field* : Celda

![[Pasted image 20230715181842.png]]

*Tuple*: Collection de valores

![[Pasted image 20230715181851.png]]

*Bag*: Collection de tuples

![[Pasted image 20230715181931.png]]


**Una relación es una *Bag* con un nombre asignado (alias), donde la mayoría de sentencias PIG Latin son creaciones de nuevas relaciones.**


#### Ejemplo de script en Pig

![[Pasted image 20230715182135.png]]

Las keywords son las palabras reservadas y los identificadores aquellos nombres que nosotros asignamos o utilizamos.
Los comentarios son como en MS o PGSQL.

#### Comandos

![[Pasted image 20230715182824.png]]
![[Pasted image 20230715182853.png]]
![[Pasted image 20230715182920.png]]

DUMP es como el show

![[Pasted image 20230715183002.png]]
![[Pasted image 20230715183011.png]]

### Tipos de datos

![[Pasted image 20230715183033.png]]

Pig realizará la mejor operación para determinar los datos, donde por ejemplo si queremos calcular la comisión de las ventas con price * 0.1, Pig asumirá que es de valor *double*.
**Es mejor especificar** el tipo de datos cuando sea posible, para evitar perder precisión y ganar en velocidad.
![[Pasted image 20230715183230.png]]

##### DATOS INVÁLIDOS

Cuando encontramos datos inválidos, Pig los sustituye por NULL, siendo un ejemplo rellenar un campo de tipo int y recibe un string.

Filtraremos pues, con IS NULL o IS NOT NULL

##### Filtrado

![[Pasted image 20230715183717.png]]

Encontramos también filtrar con expresiones regulares de Java, a través del operador **MATCHES**
![[Pasted image 20230715183815.png]]


##### Selección y generación de campos

FOREACH Y GENERATE

![[Pasted image 20230715184607.png]]

DISTINCT para eliminar registro duplicados y order by para ordenar.

![[Pasted image 20230715185314.png]]

### FUNCIONES BÁSICAS

![[Pasted image 20230715185353.png]]
