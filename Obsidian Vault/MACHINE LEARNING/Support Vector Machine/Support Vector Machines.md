
Algoritmo supervisado de ML capaz de resolver problemas lineales, no lineales y de clasificación.

Vamos a buscar el Hiperplano (subespacio plano y afín de dimensión p-1, que divide el espacio en dos mitades)

![[Captura de pantalla 2023-05-08 a las 9.58.06.png]]

*Hiperplano óptimo*

Aquel que tenga la ayor distancia mínima de las observaciones al hiperplano, el mayor margen.
(El mejor será el que esté en medio)

Los vectores soporte son los que están más cerca del hiperplano óptimo.

*Hard Margin Classifier*

Clasificadores que utilizan un hiperplano óptimo, presentan ciertos problemas:
- Son sensibles a overfitting
- Funcionan si los datos están linealmente separados
- Muy sensibles a outliers
![[Captura de pantalla 2023-05-08 a las 10.09.10.png]]

Para solucionar esto, tenemos :
*Soft margin classifier*

Hiperplano que no separa perfectamente las clases, permitiendoque algunas observaciones caigdan del lado incorrecto.
Ahora los support vectors serán tanto los que se encuentren en el margen, como los que violen el margen.

Esta flexibildiad se controla mediante C; Cuanto menor es C, más es la flexibilidad.

### *Nonlinear SVC*

Los SVC lineales funcionan bien, pero para problemas lineales que en la vida real son problemas poco frecuentes.

Una posible solución sería introducir features polinómicas, pero el problema es que estas no se adaptan bien a datasets complejos.


*Kernels*
Introducimos features polinómicas, pero sin que realmente estemos añadiendo. Esta simulació se conoce como kernel trick (Funciones que devuelven el producto escalar de dos vectoes, realizado en un nuevo espacio dimensional)

![[Captura de pantalla 2023-05-08 a las 10.19.30.png]]


