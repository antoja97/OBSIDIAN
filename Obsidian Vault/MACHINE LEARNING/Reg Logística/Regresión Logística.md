ES DE CLASIFICACIÓN !

El objetivo: Transformar el resultado de un valor continuo no acotado en una probabilidad (acotada). 


Diferencia con la regresión lineal:

![[Captura de pantalla 2023-05-04 a las 10.10.26.png]]

Los pasos que hace por detras:

1- Calcular regresión lineal.

2- Conversión a probabilidad con la función sigmoide o función logística, donde los extremos nunca se alcanzan (ni 0, ni 1).
Entre 0 y 1, y estrictamente creciente.

3- Trata de ajustar los valores para "a" y "b"

![[Captura de pantalla 2023-05-04 a las 10.15.42.png]]

¿Qué método utilizaremos?

Función de máxima verosimilitud (Maximum Likelihood)
Esto nos dice que escogeremos como valor estimado del parámetro, aquél que tiene mayor probabilidad de ocurrir según lo que hemos observado.(Binario)

Función Multiclase SoftMax: Calcula la distribución de probabilidades del evento sobre "n" eventos diferentes. (3 clases)
Hace que la suma de las probabilidades sea 1.0.
Posteriormente, para realizar la clasificación, determina cual tiene el valor más alto, que corresponderá a la clase asignada.
https://www.codificandobits.com/blog/regresion-multiclase/