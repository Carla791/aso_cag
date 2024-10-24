- Creamos el archivo
    touch script1.sh
- Le damos perminsos al archivo
    chmod u+x script1.sh
- Editamos el archivo
    nano script1.sh
    <!-- #!/bin/bash
    echo "Hola $USER"
    date '+%R'-->
- Con el comando "./script1.sh" muestra :
    - Hola vagrant
        11:19

- #!bin/bash
 ruta=`pwd`
echo $ruta

<!--` comando ` -->

- ruta=$(pwd)   
echo $ruta
 

### Comando read
 echo "Dime tu nombre"
 read nombre <!--Escribes el nombre y te lo da en respuesta en la linea siguiente -->
 echo "Hola $nombre"

<!--El comando read lee datos de usuario -->
#### -p
- Imprime "esto"
Read -p  "Dime tu nombre" nombre
echo "Hola $nombre"
#### -t
- Al cabo de x tiempo sigue
Read -p  "Dime tu nombre" -t 5 nombre
echo "Hola $nombre"
#### -n'caracteres'
 - Nos dice el numero de caracteres que hay que introducir 
Read -p  "Di un numero del 1 al 5:" -n1 num
echo 
<!--Produce un salto de linea -->
echo "Has dicho el numero  $num"
#### -s
- oculta los caracteres que vas escribiendo
Read -p  "Dime la contraseña: " pass
echo "Tu contraseña es:  $pass"




#### EJ1
1. Escribe un script en bash que pregunte a un usuario por un directorio y muestre el numero de archivos y directorios que tiene
    #!/bin/bash
    read -p "Indica  un directorio:" dir
    nitems=$(ls $dir | wc -l)
    echo "El directorio $dir tiene $nitems ficheros y subdirectorios "
   
2. Pregunta al usuario por un nombre de usuario e indica que interprete de comandos utiliza (necesitas el comando cut)
   Pregunta por el nombre de usuario e indica su shell
    <!--cat /etc/passwd | grep vagrant | cut -d : -f 7-->
    #!/bin/bash
    read -p "Indica un nombre de usuario:" user
    shell=$(cat /etc/passwd | grep $user | cut -d : -f 7)
    echo "El shell del usuario $user es $shell "

### Función if
 - Estructura
    if comando
    then
        comandos
    fi
- Ejemplo
    #!/bin/bash
    usuario=vagrant
    if grep $usuario /etc/passwd > /dev/null
    <!--Busca la variable usuario(vagrant) y las envia las salidas al fichero null-->
       <!--if grep $usuario /etc/passwd &> /dev/null manda las dos salidas al fichero -->
    then
        echo "Los ficheros bash para $usuario son"
        ls -a /home/$usuario/.b*
    fi
    
    <!--Busca los ficheros ocultos con extension .b* del usuario que se indique -->

    <!--find / > salida 2> errores -->
    <!--las salidas buenas las imprime en el fichero salida y los errores en el fichero errores -->
 #### funcion if con else
 #!/bin/bash
usuario=vagrant
if grep $usuario /etc/passwd > /dev/null
then
        echo "Los ficheros bash para $usuario son"
        ls -a /home/$usuario/.b*
else 
        echo "El usuario no existe"
fi
echo "Se acabó"
<!--Se añade que si no se encuentra que imprima q el usuario no exista-->

#### EJ2
 1. Pide al usuario un nombre de interprete (p.e. /bin/bash, /bin/sh) e indica cuantos usuario del sistema tienen ese interprete. 
   Si no hubiera ninguno muestra un mensaje diciendo que no los hay.

#!/bin/bash
read -p "Indica un nombre de shell" shell
if   grep $shell /etc/passwd > /dev/null
then
        num=$(grep $shell /etc/passwd | wc -l )
        echo "Hay $num de usuarios"
else
        echo "No hay ningun usuario con ese interprete"
fi
 
 Primero filtro el contenido del fichero , si hay alguno devuelve correcto(0) y realiza la funcion if, (sino realizaria la funcion else), utilizamos `> /dev null` para  redireccionar la salida a dev/null y que no nos salga en pantalla
### echo $?
Nos devuelve si la salida es correcta (0) o incorrecta (1)

### comando test
- Estructura
#! /bin/bash
if test condicion
then 
    comandos
fi
O tambien se puede poner 
#! /bin/bash
if [ condicion ]
then 
    comandos
fi

### Comparaciones
#### numéricas 
Tienen dos operandos 
Comparaciones:
- n1 –eq n2	Comprueba si n1 es igual a n2
- n1 –ge n2	Comprueba si n1 es mayor o igual que n2
- n1 –gt n2	Comprueba si n1 es mayor que n2
- n1 –le n2	Comprueba si n1 es menor o igual que n2
- n1 –lt n2	Comprueba si n1 es menor que n2
- n1 –ne n2	Comprueba si n1 no es igual a n2
- Ejemplo
#! /bin/bash
num=10
if [ $num -gt 8 ] <!-- mayor que, obligatorio el espacio a cada lado antes/despues []--> <!--Bien [ $num -gt 8 ], MAL [ $num -gt 8], MAL [num -gt 8]-->
then
#### EJ3
1. Pide al usuario su edad e indica:
   - Si es menor de 12 años pon " Eres un niño"
   - Si está entre 12 y 18 pon "Eres un menor de edad"
   - Si es mayor de 18 pon "Eres mayor de edad"

#!/bin/bash
read -p "Indica tu edad: " edad
if [ $edad -le 12 ]
then
        echo "Eres un niño"
fi
if [ $edad -gt 12 | $edad -lt 18 ]
then
        echo "Eres un menor de edad"
fi
if [ $edad -ge 18 ]
then
        echo "Eres mayor de edad"
fi