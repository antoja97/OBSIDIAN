
### Un modelo se crea a traves de un histórico de datos para la muestra, con el fin de que aprenda patrones para predecir el output, con el fin de que un input nuevo, sabrá dar output.

En este caso tendremos 2 inputs y el output será Y (input fumador y edad, y output el ha tenido cáncer)
![[Captura de pantalla 2023-04-18 a las 9.52.14.png]]

*Target* --> Es la variable objetivo, es decir, la variable a predecir, el output del modelo y suele ser una única variable.

*Features* --> Las que utilizamos para conseguir el output.


*El objetivo es minimizar errores, es decir, encontrar un modelo que prediga con la menor cantidad de errores posible*.


# *OJO*

No porque tenga menos error es mejor, ya que al tener menos error lo que hace es que se ajusta a los inputs dados, PERO, al entrar nuevos inputs dará muchísimo error ya que no tiene porque asemejarse a los inputs primeros.

![[Captura de pantalla 2023-04-18 a las 10.22.13.png]]

Aquí vemos justamente eso, optamos a coger el de menor error pero luego va suponer problema, ya que está demasiado ajustado.

![[Captura de pantalla 2023-04-18 a las 10.34.14.png]]

Una vez incluyamos nuevos datos, pues los vamos implementando en el modelo para ir entrenándolo y que vaya consiguiendo la minimización del error.

Tras eso tendremos que hacer el Train - test, test es lo nuevo y train es lo que tenemos.


#### *Cross Validation*

Utilizamos los datos de train en test y viceversa

![[Captura de pantalla 2023-04-18 a las 10.47.39.png]]

Con esto lo que tendremos serán 5 errores y podremos sacar la media (lo más baja posible) y la desv típica (std) (lo más baja posible)
![[Captura de pantalla 2023-04-18 a las 10.49.43.png]]


### *Overfitting*

Se trata del sobreajuste de un modelo a los datos de entrenamiento, y como consecuencia el modelo no va generalizar bien, y por ende, cuando le entren nuevos datos no va comportarse de manera correcta.

![[Captura de pantalla 2023-04-18 a las 11.03.34.png]]

### *Underfitting*

Se produce cuando entrenamos con pocos datos, ya que no será capaz de identificar los patrones para sus predicciones, y por ello NO puede generalizar bien, para cuando le lleguen datos nuevos.

![[Captura de pantalla 2023-04-18 a las 11.11.39.png]]

### El método correcto será:

Train-Test-Validation

![[Captura de pantalla 2023-04-18 a las 11.14.39.png]]

Este es para cuando queremos entrenar rápido (el de abajo)

![[Captura de pantalla 2023-04-18 a las 11.17.33.png]]

Consideraciones:

![[Captura de pantalla 2023-04-18 a las 11.21.26.png]]

**Resumen**

![[Captura de pantalla 2023-04-18 a las 11.33.13.png]]
