
K=K
N=Nearest
N=Neighbor

Es de regresión y clasificación.

Estima la probabilidad a posteriori de que un elemento x pertenezca a la clase Cj a partir de la información proporcionada por el conjunto seleccionado.

Es como decir, voy a ser lo que mas haya.
![[Captura de pantalla 2023-05-08 a las 13.30.12.png]]
Utilizamos como criterio la distancia Euclidea y es "Lazy Learn Algorithm": no entrena y simplemente guarda el dataset.

Se utilizan números impares para que no hayan empates y OBLIGATORIO ESCALAR.

Para seleccionar el valor óptimo de K es a traves de CV, es decir, de manera "iterativa", donde elegir valores pequeños de K nos lleva a límites de decisión muy sensibles o inestables. (produce overfitting)

*KNN REGRESSOR*
Se calculan las distancias de cada punto al target, eligen K-vecinos y el Output sería --> Media de los targets de los K-vecinos
