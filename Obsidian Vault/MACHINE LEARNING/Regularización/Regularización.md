
Proceso que altera ligeramente la formulación matemática de un modelo, con el fin de prevenir el overfitting.  

Una manera puede ser eliminando los gradosde una regresión polinómica o aplanando los pesos (w).

Así conseguimmos que generalice mejor y haya menos overfitting.

*RIDGE*

Añade este nuevo término a la función de costes.
El hiperparámetro alpha controla cuanto regularizamos el modelo, si alpha=0, sería regresión lineal normal, pero si alpha es muy grande, el resultado de la regresión equivaldría a una linea plana.

L2 es espacio de funciones de valor absoluto y medible

L1 medida asociada


*LASSO*

Least Absolute Shinkage ad Selection Operator Regression.

Añade un término de regularización a la función de costes, que en este caso es la norma l1 del vector de pesos.

$$Elimina los pesos de las
variables menos importantes (es una manera de hacer feature selction)
$$


*ELASTIC NET*

Término medio entre la regresión de Ridge y la de Lasso

Se comporta muy bien cuando tenemos muchas features.

Estandarización:
Se recomienda utilizar el StandardScaler de sklearn, ya que los modelos de regularización son sensibles a las escalas de las variables y de esta manera entrenan mucho más rápidos.

EN LA CARPETA DE REGULARIZACIÓN, EN EL NOTEBOOK EJERCICIO 4 Y 5, VEMOS COMO HACEMOS MODELO, ENTRENAMOS, PREDECIMOS (EN EL 4 ESCALAMOS)



