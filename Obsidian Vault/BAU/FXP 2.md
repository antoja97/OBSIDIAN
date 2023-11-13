Una vez reprocesado , se puede resolver el ticket, pinchando en la incidencia y donde pone State, darle a resolved.

![[Pasted image 20231110130936.png]]

En resolution reprocess poner el número del reproceso para que se pueda ver mejor los esclarecimientos de los comentarios.


Estos días suelen ser problemas de origen, abrimos ticket y pedimos reproceso (CASI SIEMPRE ES EL MISMO DE ORIGEN)

Monitorizar la malla por control-m web, sql0 trae los datos de api y abajo parte Qlik.


# FORMA DE TRABAJAR DE ALE

![[Pasted image 20231110132149.png]]

Abrir el log del fallo en notepad ++, buscar el dag_name o dag-name, me voy a Airflow, veo el que ha fallado (1 hora más) pincho la tarea que falló, en este caso count 0 porque no hay datos.

Si quiero probar , hay que preguntar a CCB para que vuelvan el job con los parámetros que se digan.



