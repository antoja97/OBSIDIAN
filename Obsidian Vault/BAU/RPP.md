
![[Pasted image 20231110132953.png]]

Se lanzan los 11 jobs, y suelen fallar 1-2 , y suelen ser fallos de concurrencia, ya que se lanzan a la vez, y es porque alguno no entra o así.

Buscar el dag, ver si han ido los 11, rendered template, y buscar el parámetro que pertenecerá a uno de los JOBS y así podré reconocerlo.

Se puede ver mejor en el control-m estático que en el WEB y vemos el valor del job y ver la tabla de la que tira.

![[Pasted image 20231110133551.png]]

Ahí pediría el reproceso.


## OTRO FALLO HABITUAL

En el de abajo de los 11 jobs, el de la izquierda del todo.

Vemos el log del que ha fallado, pero que a lo mejor no es y ha sido simplemente por tiempo, miramos en databricks de que haya ido todo bien.

Decir que no hace falta reprocesar ya que ha sido por error de tiempo.


### Esto son las prioridades

Prio 4 :24h,
Prio 5: 48h,
Incidencia: 5 días