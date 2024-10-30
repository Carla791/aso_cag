## Pasos
### Permisos de usuarios
1. Crea el directorio pr0201 dentro de tu directorio personal y dentro de él crea los directorios dir1 y dir2 ¿Cuáles son los permisos del directorio dir1? No pongas una captura, explica quiénes tienen permisos sobre el directorio y qué pueden hacer en él.
   - El propietario y el grupo al que pertenece tienen permisos de lectura escritura y ejecución. El resto de usuarios tienen permisos de lectura y ejecución.
      - Comandos:
        - mkdir pr0201
        - mkdir pr0201/dir1 pr0201/dir2
        - ls -l -R
<!--Usamos el comando mkdir "nombre del directorio" para crear los directorios y el comando ls -l para ver los permisos de los directorios -->
2. Utilizando la notación simbólica, elimina todos los permisos de escritura (propietario, grupo, otros) del directorio dir2.
    - Comandos:
      - chmod a-w pr0201/dir2
<!--Usamos el comando chmod para cambiar los permisos del directorio "a" todos los usuarios "w" permisos de escritura "dir" nombre del directorio, utilizamos el comando ls para comprobarlo -->
3. Utilizando la notación octal, elimina el permiso de lectura del directorio dir2, al resto de los usuarios.
    - Comandos: 
      - chmod 551 pr0201/dir2
<!--Usamos el comando chmod para cambiar los permisos del directorio dir2 en modo octal 5=r-x 1=--x, utilizamos el comando ls para comprobarlo -->
4. ¿Cuáles son ahora los permisos asociados a dir2?
   - EL directorio dir2 tiene los permisos de ejecución y lectura para el propietario y el grupo del objeto y permisos de ejecución para el resto de usuarios. 
<!--Utilizamos el comando ls -l -R   dr-xr-x--x 2 vagrant vagrant 4096 Oct  1 06:50 dir2-->
5. Crear bajo dir2, un directorio llamado dir21.
    - No nos deja porque no tenemos el permiso requerido.
<!--Comando mkdir pr0201/dir2/dir21.     Necesitamos el permiso de escritura-->
6. Concédete a ti mismo permiso de escritura en el directorio dir2 e intenta de nuevo el paso anterior.
    - Comandos:
      - chmod u+w pr0201/dir2
      - mkdir pr0201/dir2/dir21 
<!--Utilizamos chmod para modificar losmpermisos del directorio "u" propietario "+" "w"permisos de escritura, utilizamos mkdir para crear el directorio y ls -R para comprobarlo-->
### Notación octal y simbólica
1. Supón que el fichero ~/file tiene los permisos rw-r--r--. Escribe el comando o comandos que necesitarías para establecer los siguientes permisos en el fichero anterior utilizando notación simbólica.
   <!--u para el usuario, g para el grupo, o para otros, a para todos los anteriores y después r para permisos de lectura, w para permiso de escritura, x para permiso de ejecución. El siguiente carácter se utiliza para indicar si quieres añadir el permiso a los existentes (+), quitar el permiso de los existentes (-), o establecer el permiso a un valor (=).-->
    - rwxrwxr-x : 
      - chmod ug=rwx file
      - chmod o+x file
    - rwxr--r-- :
      - chmod u+x file
    - r--r----- : 
      - chmod u-w file
      - chmod o-r file
    - rwxr-xr-x : 
      - chmod a+x file
    - r-x--x--x : 
      - chmod go-r file
      - chmod a+x file
    - -w-r----x :
      - chmod uo+r file
      - chmod o-x file
    - -----xrwx : 
      - chmod o=rwx file
      - chmod u-rw file
      - chmod g-r file
      - chmod g+x file
    - r---w---x : 
      - chmod go-r file
      - chmod u-w file
      - chmod g+w file
      - chmod o+x file
    - -w------- : 
      - chmod a-r file
    - rw-r----- : 
      - chmod o-r file
    - rwx--x--x : 
      - chmod a+x file
      - chmod go-r file
2. Escribe el comando que necesitarías para establecer los siguientes permisos en el fichero anterior utilizando notación octal.
     <!--La notación octal consiste en asignar a cada grupo de permisos un dígito octal (3 bits). Cada bit de ese dígito corresponderá a cada uno de los permisos diferentes disponibles.-->
    - rwxrwxrwx :
      - chmod 777 file
    - --x--x--x :
      - chmod 111 file
    - r---w---x :
      - chmod 421 file 
    - -w------- :
      - chmod 200 file 
    - rw-r----- :
      - chmod 640 file 
    - rwx--x--x :
      - chmod 711 file
    - rwxr-xr-x :
      - chmod 755 file
    - r-x--x--x :
      - chmod 511 file 
    - -w-r----x :
      - chmod 241 file
    - -----xrwx :
      - chmod 017 file 

### El bit setgid
1. Crea un grupo llamado asir y los usuarios {iniciales}1 e {iniciales}2, donde {iniciales} son las iniciales de tu nombre. Haz que los usuarios pertenezcan al grupo.
    - Comandos:
      - sudo groupadd asir
      - sudo adduser cag1
      - sudo adduser cag2
      - sudo usermod -g asir cag1
      - sudo usermod -g asir cag2
      - id cag1
      - id cag2
<!--El comando groupadd sirve para crear un grupo -->
<!--El comando adduser crea un usuario contraseña: 1234-->
<!--El comando usermod modifica la mayoría de campos del fichero etc/passwd  -g modifica el grupo-->
2. Crea el directorio /compartido y asigna propietario: root como usuario propietario y asir como grupo propietario.
    - Comandos:
      - sudo mkdir /compartido
      - sudo chown root compartido
      - sudo chown .asir compartido
<!--El comando chown modifica el usuario propietario y el gruopo propietario de un fichero o directorio  con la estructura: chown [usuario] [fichero] o chown [grupo] [fichero]-->
3. Asigna al directorio creado permisos de lectura, escritura y ejecución para el usuario y el grupo propietario. El resto de usuarios no tendrá ningún tipo de permiso.
    - Comandos:
      - sudo chmod 770 compartido
<!--El comando chmod modifica los permisos el 7 da todos los permisos y el 0 ninguno-->
4. Establece el bit setgid en el directorio y verifica que se haya asignado.
    - Comandos:
      - sudo chmod g+s compartido
      - ls -s -l
<!--El comando chmod modifica los permisos del directorio "g+s" establece el set group id-->  
5. Inicia sesión con usuario1, accede al directorio y crea un fichero llamado fichero1 con algo de contenido. Comprueba los permisos del fichero que has creado.
   - Comandos:
     - su cag1(1234)
     - cd /compartido
     -  echo "Hola mundo. Bienvenidos."> fichero1.txt
     -  ls -l 
<!--El comando su se utiliza para iniciar sesion con otro usuario-->  
<!--El comando echo "Texto"> fichero.txt  crea un fichero con texto-->  
<!-- -rw-r--r-- 1 cag1 asir fichero1.txt Hay permisos de lectura y escritura para el propietario y para el grupo y el resto de usuarios solo de lectura-->
6. Ahora inicia sesión con usuario2 y comprueba si puedes acceder a /compartido/fichero1 y si puedes añadirle contenido.
   - Comandos:
     - su cag2(1234)
     - vi fichero1.txt
     - cat fichero1.txt
    - Podemos acceder y añadir contenido al archivo gracias al SGUI que establecimos en el directorio
<!--Una vez entremos en el editor vi pulsamos "a" para escribir , "ESC" para salir al modo comandos y :wq para guardar los cambios-->  
<!--Con el comando cat visualizamos el contenido del archivo-->  
7. Responde las siguientes preguntas:
  1. ¿Qué ventajas tiene usar el bit setgid en entornos colaborativos?
      - En el caso de los directorios, garantiza que los nuevos archivos creados dentro del directorio hereden el grupo del directorio, no del usuario que creó el archivo. 
      Esto es especialmente útil para entornos colaborativos en los que un grupo de usuarios necesita compartir archivos, pero también garantiza la propiedad adecuada del grupo por motivos de seguridad y organización.

  2. ¿Qué sucede si no se aplica el bit setgid en un entorno colaborativo?
    - Si no se aplica cada directorio creado pertenecería al usuario individual que lo ha creado en vez de al grupo. Y tendriamos que añadir el grupo a cada directorio creado.

8. Cuando hayas acabado, limpia el sistema eliminando los usuarios y el directorio creado para la práctica
    - Comandos: 
      - sudo userdel -r cag1
      - sudo userdel -r cag2 
      - sudo rm -r compartido
<!--El comando userdel sirve para eliminar un usuario --> 
<!-- El comando rm sirve para eliminar directorios con "-r" eliminamos recursivamente los subdirectorios -->  
### El sticky bit 
1. Crea el directorio /compartido con todos los permisos para todos los usuarios.
    - Comandos: 
      - sudo mkdir /compartido
      - sudo chmod 777 compartido
<!--El comando mkdir crea un directorio--> 
<!--El comando chmod modifica los permisos, "7"= todos los permisos--> 
2. Crea dos usuarios {iniciales}1 e {iniciales}2
    - Comandos:
      - sudo adduser cag1
      - sudo adduser cag2
<!--El comando adduser crea un usuario contraseña: 1234-->
3. Vamos a probar primero el funcionamiento sin el sticky bit. Inicia sesión con el primer usuario, crea un fichero y luego, con el segundo usuario, intenta eliminarlo.
   - Comandos:
     - su cag1(1234)
     - cd /compartido
     -  echo "Bienvenidos a mi nave"> fichero1.txt
     -  su cag2(1234)
     -  rm fichero1.txt
    - Si se puede eliminar
<!-- El comando su para iniciar sesión en otro usuario --> 
<!-- El comando echo para crear un archivo con texto --> 
<!-- El comando rm sirve para eliminar archivos --> 
4. Ahora establece el sticky bit en el directorio y verifica que se ve en los permisos.
   - Comandos:
     - sudo chmod +t compartido
     - ls  -s -l 
<!--El comando chmod modifica los permisos del directorio "+t" establece el Sticky Bit--> 
<!--  4 drwxrwxrwt   2 root root       4096 Oct  3 11:22 compartido-->  
5. Vuelve a iniciar sesión con el primer usuario, crea un fichero e intenta eliminarlo con el segundo usuario.
    - Comandos:
      - su cag1(1234)
      - cd /compartido
      -  echo "Bienvenidos "> fichero1.txt
      -  su cag2(1234)
      -  rm fichero1.txt
    - No se puede eliminar.
<!-- El comando su para iniciar sesión en otro usuario --> 
<!-- El comando echo para crear un archivo con texto --> 
<!-- El comando rm sirve para eliminar archivos --> 
6. Responde las siguientes preguntas:
    1. ¿Qué efecto tiene el sticky bit en un directorio?
      - Su objetivo es que solo el usuario propietario pueda eliminar o renombrar un archivo o directorio.Sirve para evitar el borrado accidental de archivos o directorios.
    2. Si tienes habilitado el sticky bit, ¿cómo tendrías que hacer para   eliminar un fichero dentro del directorio?
      - Se podria borrar por el usuario root(sudo rm "directorio") o desde el usuario que creó el fichero.
<!-- -->  
<!-- -->  
[Volver al índice](../../index2.md)