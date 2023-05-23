Combinan decisiones de múltiples modelos para mejorar su precisión y estabilidad (minimizar Bias y Varianza, donde pueden algunos modelos querer bajar uno u otro)

### Tipos
1- Bagging (Bootstrap Aggregating)
- Voting Classifier
- Bagging Classifier
- Random Forest

2- Boosting
- AdaBoost
- GradientBoost
- XGBoost

![[Captura de pantalla 2023-05-10 a las 11.01.15.png]]


### *Bootstrap*

Es un mecanismo propio de estadística que se centra n el remuestreo de datos con reemplazamiento, dentro de una muestra aleatoria o al azar.

###### *Algoritmos de votación*

![[Captura de pantalla 2023-05-10 a las 11.10.58.png]]

¿Cómo se realizan las predicciones?

- Clasificación - Hard Voting --> Calcula la moda
- Clasificación - Soft Voting --> Calcula la media y establecerá a través de los umbrales.
- Regresión --> Calcula la media de todos los outputs
![[Captura de pantalla 2023-05-10 a las 11.09.55.png]]

*Bagging*

Cojo mi muestras, elijo cuantos modelos quiero entrenar y saco las muestras que queramos, entrenamos sobre esas muestras, decimos y ensamblamos.

*Random Forest*

Aplicar Bagging sobre algo mediante árboles de decisión.
RandomForestClassifier y RandomForestRegressor

Pasos (Lo que ocurre por detras):
1- Cogemos una cantidad de arboles que entrenaremos.
2-Cada árbol escoge conjunto aleatorio de features para realziar cada split y puede ser configurado por sklearn.
3- Aplicamos Bootstrapping, es decir, cada árbol entrena con una muestra aleatoria con un reemplazamiento del conjunto de train.
4-Una vez ntrenado, aplicamos sistema de votación de bagging para las predicciones.

##### *Boosting*

Los modelos se entrenan secuencialmente y por tanto existe una dependencia entre ellos.
Básicamente los modelos van intentando mejorar su predecesor, recibiendo los errores del mismo, e intentando mejorar su resultado.

Los más utilizados son:
- AdaBoost
- Gradient Boosting
- XGBoost

La diferencia con RandomForest es que se puede paralizar en Big Data y este no.

El Gradient Boost trabaja sobre árboles de decisión, ajustando y minimizando los errores del modelo predecesor.