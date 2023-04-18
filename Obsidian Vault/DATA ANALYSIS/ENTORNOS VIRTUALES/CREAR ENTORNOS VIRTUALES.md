
*1* : Tenemos que situarnos en la raiz main y ahí en terminal escribimos:
viartualenv (nombre que queramos).

O

python3 -m venv (nombre que queramos)
y después source (nombrequehemospuesto)/bin/activate

*2* -Ya a la izquierda nos aparecerá entre paréntesis el nombre que le hemos puesto y estaremos ya en el entorno virtual.

*3*- Tras esto abajo a la izquierda nos vamos al intérprete y veremos que tenemos el de venv, asegurándonos que está marcada ahí.

*4*- Si ejecutamos nos pondrá que nos falta librerías, por lo que vamos instalándolas.

*5*-Una vez instaladastodas, ponemos en terminal python3 main.py ( en este caso porque el archivo se llama así)

*6*- Para hacer que todas estas librerías se queden guardadas en este entorno ponemos en terminal :  pip freeze > requirements.txt

*7*- Para salir del entorno ponemos deactivate.

*8*- La borramos si queremos

*9*- Cuando veamos que hay un requirements, encendemos entorno virtual y ahora con esto, pondremos en terminal : pip install -r \requirements.txt.   (la r así tiene una barra \ )
Con esto se nos instalará todo sin necesidad de tener que importar todo lo que nos vaya pidiendo


## ESTO SE ENCUENTRA EN EL PROYECTO DE HUNDIR LA FLOTA 
