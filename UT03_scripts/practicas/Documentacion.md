# Condicional if
1. Comprobación de número par o impar
Escribe un script que solicite al usuario un número y determine si es par o impar utilizando una estructura if.
 - read -p "Indica un número " num
    if [ $(($num%2)) -eq 0 ]
    then
        echo "El numero $num es par"
    else 
        echo "El número $num es impar"
    fi    
    <!--El numero que se introduce se convierte en una variable que dividida por 2 tiene que dar 0 para ser un número par y sino el número será impar-->
1. Verificación de archivo
Crea un script que compruebe si un archivo (cuya ruta pedirá al usuario por teclado) existe y si tiene permisos de lectura. Muestra un mensaje adecuado para cada caso.
   - read -p "Indica la ruta de un archivo: " ruta 
   if test -r $ruta
   then
           echo "El archivo existe y tiene permisos de lectura"
   else 
           echo "El archivo no existe o no tiene permisos de lectura"
   fi
<!-- Utilizamos la funcion if y el comando test -r "archivo" para comprobar si el archivo existe y tiene permisos de lectura sino el archivo no existe o no tiene permisos de lectura-->
3. Comparación de dos números
Realiza un script que solicite dos números al usuario y los compare, mostrando cuál es mayor, o si son iguales.
