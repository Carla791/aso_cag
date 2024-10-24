# Programación de tareas con cron
## Pasos
1. ¿Qué orden pondrías en crontab en los siguientes casos?
   <!--Utilizariamos sudo crontab -e para editar las tareas-->
   - La tarea se ejecuta cada hora
     - @hourly [usuario] [tarea]
     - 0 * * * * [usuario] [tarea]
   - La tarea se ejecuta los domingos cada 3 horas
     - 0 */3 * * 0 [usuario] [tarea]
   - La tarea se ejecuta a las 12 de la mañana los días pares del mes.
     - 0 12 */2 * * [usuario] [tarea]
   - La tarea se ejecuta el primer día de cada mes a las 8 de la mañana y a las 8 de la tarde.
     - 0 8,20 1 * * [usuario] [tarea]
   - La tarea se ejecuta cada media hora de lunes a viernes.
     -  */30 * * * 1-5 [usuario] [tarea]
   - La tarea se ejecuta cada cuarto de hora, entre las 3 y las 8, de lunes a viernes, durante todo el mes de agosto
     - */15 3-8 * 8 1-5 [usuario] [tarea]
   - La tarea se ejecuta cada 90 minutos
     - 0 */3 * * * [usuario] [tarea]
     - 30 1-23/3 * * * [usuario] [tarea]
2. ¿Cómo compruebas si el servicio cron se está ejecutando?
   - sudo systemctl status cron
   - ps aux | grep cron
    <!--Estos comandos nos dira si cron esta activo-->
3. ¿Cuál es el efecto de la siguiente línea crontab?
   - */15 1,2,3 * * * who > /tmp/test
     - La tarea se ejecuta cada cuarto de hora, a la 1, las 2 y las 3 de la madrugada, todos los días. Y guardara la lista de usuarios conectados en el archivo /tmp/test.
4. Indica la ruta del fichero crontab del sistema
   - /etc/crontab
5. ¿Qué ficheros controlan los usuarios que pueden utilizar el crontab?
  - Los ficheros cron.allow y cron.deny
<!--Cron.allow:los usuarios que están listados en el fichero pueden crear, editar, mostrar o eliminar ficheros crontab. -->
<!--Cron.deny:los usuarios que están listados en el fichero no pueden crear, editar, mostrar ni eliminar ficheros crontab. -->
6. Excepcionalmente se debe iniciar una tarea llamada script.sh todos los lunes a las 07:30h antes de entrar en clase ¿Cómo lo harías?
  - 30 7 * * 1 /home/vagrant/script.sh
  <!--Se añade la ruta absoluta del fichero-->
7. Se ha cancelado la tarea. ¿Cómo listar y luego, suprimir la tarea?
   - crontab -l
   - crontab -r
  <!--Se utiliza el comando crontab, usamos -l para listar la tarea y -r para suprimir la tarea-->
8. Ejecuta el comando ps -ef para el usuario root cada 2 minutos y redirecciona el resultado a /tmp/ps_result sin sobrescribir los antiguos.
  - */2 * * * * sudo ps -ef > /tmp/ps_result
  <!--Se utiliza el comando sudo para que lo ejecute el usuario root-->
9. Verifica la lista de tareas en crontab
  - crontab -l
10. Espera unos minutos y comprueba el resultado en /tmp
  - Si nos sale
11. Crea el usuario asir2 y prohíbele utilizar el crontab.
  - sudo adduser asir2(1234)
  - sudo touch cron.deny
  - sudo nano cron.deny
  <!--Creamos el usuario asir2-->
  <!--Creamos el archivo cron.deny-->
  <!--Editamos el archivo cron.deny, añadiendo el usuario-->
12. Verifica que el usuario asir2 realmente no puede utilizar crontab
  - crontab -e
  <!--Probamos a editar un archivo crontab y no nos lo permite-->
13. Programa crontab para que cada día a las 0:05 se eliminen todos los ficheros que se encuentran en el directorio /tmp.
  - 5 0 * * * rm -r /tmp
  <!--Se utiliza el comando rm -r para borrar recursivamente-->
14. Programa una tarea en el sistema que se lance de lunes a viernes a las 9 de la mañana durante los meses de verano (julio, agosto y septiembre) que escriba en un fichero la hora actual (comando date, aunque tienes que mirar la ayuda para elegir un formato comprensible) seguido del listado de usuarios que hay conectados en ese momento en el sistema (comando who)
  - * 9 * 7-9 1-5 date + '%T' > /tmp/file ; who >>/tmp/file 
15. El servicio cron se ayuda de una serie de ficheros y directorios que se encuentran en el directorio /etc. Explica la función de cada uno de los siguientes ficheros/directorios:
  - cron.d:permite a los usuarios realizar tareas y ejecutarlas automáticamente a una hora determinada
  - cron.allow:los usuarios que están listados en el fichero pueden crear, editar, mostrar o eliminar ficheros crontab.
  - cron.deny:los usuarios que están listados en el fichero no pueden crear, editar, mostrar ni eliminar ficheros crontab.
  - cron.daily: cualquier script que se guarde en este fichero se ejecutará una vez cada día.
  - cron.hourly: cualquier script que se guarde en este fichero se ejecutará una vez cada hora.
  - cron.monthly: cualquier script que se guarde en este fichero se ejecutará una vez cada mes.

