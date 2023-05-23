
Las categorías no se pueden ordenar, ni sumar, ni restar...

OJO:
Pandas por defecto entiende que un número es de tipo numérico.
Si un número es una categoriá, tenemos que decírselo nosotros explícitamente. Los strings son de tipo objeto.

#### Codificación de categorías
Lo que hace es asociar una categoría a un número, respetando *NO darle más peso a una etiqueta que a otra*.

5 formas distintas de codificar:
- One-hot
- Dummy
- Effect
- Hash
- Estadístico de etiqueta
Nos interesa manejar números porquelos ordenadores trabajn muy bien con números


### One-Hot encoder
Cada valor distinto dentro de la columna se convierte en una nueva columna binaria.![[Captura de pantalla 2023-05-12 a las 12.14.57.png]]

INCONVENIENTE!

Dummy variable trap
![[Captura de pantalla 2023-05-12 a las 12.24.38.png]]

Solución!

Dummy encoder
![[Captura de pantalla 2023-05-12 a las 12.27.18.png]]

