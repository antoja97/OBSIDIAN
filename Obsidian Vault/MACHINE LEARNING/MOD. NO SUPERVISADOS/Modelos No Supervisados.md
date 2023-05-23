
Tenemos un conjunto de piedzas para una linea de producion y queremos montar modelo de ML que prediga si la pieaza está defectuosa.

Montaremos entncesmodelo automático que las clasifique, pero , NO TENEMOS DATOS ETIQUETADOS, ya que son imágenes.


#### *Feature Reduction*

*Curse of Dimensionality*

El número de muestras que se necesitan para estimr una función arbitraria con un cierto nivel de precisión, crece exponencialmente con el número de inputs/dimensiones/variables de la función.

Este fenómeno afecta mucho a la dispersión y la cercanía de los datos.

Menos variables, menos ruido y nuestras métricas mejorarán.
Lo malo es que perderemos información.

![[Captura de pantalla 2023-05-15 a las 10.17.37.png]]. 

*Clustering*
Se pretende agrupar los datos sin etiquetar en diferentes grupos (o cluster), de manera automática.
Estos algoritmos buscan patrones y similitudes en los datos y los agrupan en k grupos, siendo k un parámetro dado.

Clasificación vs Clustering:
En clustering no tenemos eld ato etiquetado, y por tanto es el modelo que clasificas losd atos en k clases. No se sabe que es cada clase, pero agrupa los datos según similitudes.


##### *Algoritmos de Clustering*

![[Captura de pantalla 2023-05-15 a las 10.54.41.png]]

*Métricas*

![[Captura de pantalla 2023-05-17 a las 9.57.07.png]]

Compacidad --> La distancia entre cada punto (lo más cercano) Garantia de que lo que cae en el mismo cluster sean similares.

Lo mejor es que A sea lo más baja posible y B lo más alta posible

Fórmula de separabilidad, con el fin de que sea lo más compacto posible.

![[Captura de pantalla 2023-05-17 a las 10.03.37.png]]

Separabilidad --> La distancia es más lejana (pueden caer algunos que haya sido por error)


Con valores absolutos se le da menos importancia a los outliers.


