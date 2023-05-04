
Web explicación clara:
https://www.iartificial.net/precision-recall-f1-accuracy-en-clasificacion/

Aprendizaje supervisado:
- Regresión
- Clasificación

Aprendizaje no supervisado:
- Clusterización
- Reducción de dimensionalidad

Aprendizaje por refuerzo


## Algoritmos de clasificación

Son algoritmos de aprendizaje supervisado cuyo objetivo es predecir etiquetas de clase categóricas.

Los más comunes:
Regresión logística, árbol de decisión, KNN, Naive Bayes, SVC, Random Forest y Deep Learning


#### Accuracy (exactitud en este caso)

Cantidad de aciertos vs fallos --> correct predictions / all predictions
NO ES LA MEJOR MÉTRICA

La importancia de la métrica:
calculamos la accuracy de gente que tienen diabetes vs los que no tienen:
97% de precisión!! Qué bueno!
NO
No es representativa.
¿Soluciones?
1-Cambiar métrica
2-Conseguir más datos
3- Resampling: o bien ponemos copias de los elementos de la clasedesfavorecida, o eliminamos registrosde l más poblada.
4- Generar datos sintéticos.

#### Precision
De todos los que he predicho 1, cuantos en realidad son uno.

#### Recall o sensibilidad

Positivos que he sacado bien vs todos los positivos

![[Captura de pantalla 2023-05-03 a las 12.53.09.png]]

![[Captura de pantalla 2023-05-03 a las 12.56.24.png]]

#### F1-Score
Combinación de precisión y recall
![[Captura de pantalla 2023-05-03 a las 13.05.42.png]]

## Escoger métrica

![[Captura de pantalla 2023-05-03 a las 13.14.03.png]]

### Predicción probabilística

![[Captura de pantalla 2023-05-03 a las 13.16.36.png]]

## Curva ROC
Nos indica como de bueno es nuestro modelo para distinguis las clases, la cual va de 0 a 1.

Lo compone:
-Eje X: FPR (False Positive Rate) --> 0s identificados erróneamente como 1s
-Eje Y: TPR (True Positive Rate)--> Es lo mismo que recall: Positivos que había clasificado bien vs todos los positivos que había
-AUC (Area Under the Curve) --> Todo lo que se encuentra por debajo de la curva, que mide el acierto en la predicción de eventos binarios.

¿Cómo interpretamos?
1-Cuanto mayor es AUC, más se acerca la curva a la esquina superior izquierda, mejor es el clasificador.
2- La linea recta del medio representa un clasificador aleatorio, por tanto, cuanto más cerca de esa linea, peor.
3- Si la curva queda por debajo del random classifier, quiere decir que nuestro modelo lo hace peor que un clasificador aleatorio.
4-Si la curva forma un ángulo recto, tienes un clasificador perfecto... ospecha si has hecho algo mal.


![[Captura de pantalla 2023-05-03 a las 13.30.45.png]]