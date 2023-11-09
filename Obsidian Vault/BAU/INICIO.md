
FX Position son ingleses, muy pesados.

Control-M donde se ven los jobs a tiempo real y se trabaja con esto fundamentalmente.
Un ticket es un job que ha fallado.
Se ve la malla , conectados uno a otro.

**LSQL1** (la mia) (las de abajo es de Qlik, Janna y Antonio) es el motor principal que falla a diario, principalmente de seguridad.
Los  jobs de backoffice acounting están teniendo mucho delay, desde origen.
Se lanza sobre las 9.15 de la mañana y la tabla no ha recibido datos a esa hora.

Me pasará la lista y puedo preguntar a Fran López López y Catarina para que me ayuden, cuales tickets son míos en caso de duda.

![[Pasted image 20231108162407.png]]


PLIQUICKT003D/G-GBMSA-P-800031932 - Odate: 2023/11/03

PLIQUICKT003D --> este es el job que está en fallo

G-GBMSA-P-800031932 --> no me va servir, código orbis

Odate: 2023/11/03 --> fecha en la que ha fallado


**EN EL NÚMERO INC.... PUEDO PINCHAR Y VER DIRECTAMENTE EL FALLO**

**ABRO EL SCRIPT CON UN NOTEPAD QUE TENDRÉ QUE DESCARGAR, DONDE ESTARÁ EL LOG**

pongo dag_name para buscar el dag que falla y miro a ver que es (normalmente es lo que falla)
puede ser por hdfs (aunque sea muy poco)


![[Pasted image 20231108162927.png]]

**PUEDE SER QUE HAYA HABIDO ERROR EN AIRFLOW O DIRECTAMENTE NO HAYA NI LLEGADO A AIRFLOW**

AL VER EL LOG BUSCO EL ERROR Y TENEMOS QUE IR A S3.

![[Pasted image 20231108163057.png]]

LANDING Y VER SI HAY DATOS, BUSINESS , STAYING O LAGO (LAKE) 
VER CÓDIGO, REPOSITORIO, TABLAS.

SI EN LANDING NO HAY DATOS HAY QUE PONERNOS EN CONTACTO CON LA GENTE DE DATALAKE.


COSAS DE CONFLUENCE PARA VER POR MI PARTE:
[https://confluence.alm.europe.cloudcenter.corp/pages/viewpage.action?spaceKey=CIBCOEBDC&title=Initiatives+Documentation](https://confluence.alm.europe.cloudcenter.corp/pages/viewpage.action?spaceKey=CIBCOEBDC&title=Initiatives+Documentation "https://confluence.alm.europe.cloudcenter.corp/pages/viewpage.action?spacekey=cibcoebdc&title=initiatives+documentation")



# QUE HACER CUANDO UN TICKET NO ES MIO

Normalmente suelen poner descripción y no detallan bien la información.

Pedir datos, tablas, capturas de pantalla...

Se puede poner en on hold (en espera)  si a los 2-3 días de margen, no responden ya nos dirán Sara y Fran , pero se suele cerrar.


# CUANDO VEA UN TICKET MIO, ME LO PONGO IN PROGRESS (BUENAS PRÁCTICAS)



El control-M web, tiene histórico de 2 semanas y como base de datos, y ofrece datos a tiempo real (para ver si falla más días, el tiempo de duración, anomalías, parámetros).

Puede haber errores por magia, que cambien algo, podemos ver condiciones de entrada y salida.

El normal es más visual, buscando JOB, action, neighborhood, se abre y el esquema nos mostrará, más en profundidad.


# HUE

El error que sale todos los días, suele mirarlo en Impala que es más rápido.

CONTROL-M, AIRFLOW, DATABRICKS, HUE Y S3.







