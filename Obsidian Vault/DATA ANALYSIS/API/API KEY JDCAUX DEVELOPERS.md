
**ESTO SE ENCUENTRA EN DATA ANALYSIS, DATA SOURCES, APIS Y VA CON EL EJERCICIO DE SEVICI** 


Comenzamos con:

![[Captura de pantalla 2023-03-22 a las 11.29.32.png]]

Despues sacalos las keys estableciendoselo a una variable y en este caso nos interesa "features"

![[Captura de pantalla 2023-03-22 a las 11.30.49.png]]

Ahora tenemos que hacer esto siempre ya sea por lista por comprensión o bucle.

-Lista por comprensión:

![[Captura de pantalla 2023-03-22 a las 11.31.57.png]]

-Bucle:

![[Captura de pantalla 2023-03-22 a las 11.32.21.png]]


Tras esto convertiremos a DataFrame para poder trabajar con eso.

![[Captura de pantalla 2023-03-22 a las 11.32.58.png]]




API KEY
18af6e51bc6f9cd8292d6c5e143a9f8aca7be204


Aquí lo que hacemos es meter nuestra api key y despues el url de get contract que es ese.

![[Captura de pantalla 2023-03-22 a las 10.36.09.png]]

Esto sería para obtener del tirón sin especificar.


#SegundoEjemplo

Aquí sacamos las estaciones que hay en Sevilla.

Si quisieramos cambiarle para que nos diese una estación tal cual, tendriamos que buscar el índice o el nombre y sería:

Por ejemplo lemetemlos el 10

-Por índice --> stations/10?

station_name="san bernarndo"
-Por variable --> stations/{station_name}?

![[Captura de pantalla 2023-03-22 a las 10.49.35.png]]


#CreafunciónGETSTATION

Contando con la anterior api_key y el anterior contra_name="seville",

Creamos la función para que nos de la estación.

![[Captura de pantalla 2023-03-22 a las 10.58.48.png]]

#Geopy

Para encontrar la distancia geodésica

![[Captura de pantalla 2023-03-22 a las 11.17.33.png]]