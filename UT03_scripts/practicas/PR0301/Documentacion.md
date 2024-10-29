# Condicional if
## Comprobación de número par o impar
1. Escribe un script que solicite al usuario un número y determine si es par o impar utilizando una estructura if.

``` bash
#!/bin/bash
 read -p "Indica un número " num
    if [ $(($num%2)) -eq 0 ]
    then
        echo "El numero $num es par"
    else 
        echo "El número $num es impar"
    fi   
``` 
<!--El numero que se introduce se convierte en una variable que dividida por 2 tiene que dar 0 para ser un número par y sino el número será impar-->
## Verificación de archivo
2. Crea un script que compruebe si un archivo (cuya ruta pedirá al usuario por teclado) existe y si tiene permisos de lectura. Muestra un mensaje adecuado para cada caso.

``` bash
#!/bin/bash
read -p "Indica la ruta de un archivo: " ruta 
if test -r $ruta
then
      echo "El archivo existe y tiene permisos de lectura"
else 
      echo "El archivo no existe o no tiene permisos de lectura"
fi
```
<!-- Utilizamos la funcion if y el comando test -r "archivo" para comprobar si el archivo existe y tiene permisos de lectura sino el archivo no existe o no tiene permisos de lectura-->
## Comparación de dos números
3. Realiza un script que solicite dos números al usuario y los compare, mostrando cuál es mayor, o si son iguales.
   
```bash
#!/bin/bash
read -p "Indica un numero: " num1
read -p "Indica otro numero: " num2

if [ $num1 -gt $num2 ]
then
        echo  "$num1 es mayor que $num2"
elif [ $num1 -lt $num2 ]
then
        echo "$num2 es mayor que $num1"
else
        echo "Los dos números son iguales"
fi
```

## Validación de contraseña
4. Escribe un script que solicite al usuario una contraseña y verifique si coincide con una contraseña predefinida (que estará almacenada en una variable de tu script). Si es correcta, muestra un mensaje de éxito, de lo contrario, indica que es incorrecta.

```bash
#!/bin/bash
predef="1234"
read -sp "Introduce la contraseña: " pwd
echo

if [ $pwd == $predef ]; then
    echo "Contraseña correcta"
else
    echo "Contraseña incorrecta"
fi
``` 

## Comprobación de directorio
5. Crea un script que compruebe si un directorio existe y si tiene permisos de escritura. Si el directorio no existe, crea uno nuevo.
   
```bash
#!/bin/bash
read -p "Introduce el nombre del directorio: " dir

if [ -d $dir ]; then
    if [ -w $dir ]; then
        echo "El directorio existe y tiene permisos de escritura"
    else
        echo "El directorio existe pero no tiene permisos de escritura"
    fi
else
    mkdir $dir
    echo "El directorio no existía, pero ha sido creado"
fi
```

## Verificar si el usuario es root
6. Haz un script que verifique si el script está siendo ejecutado por el usuario root, mostrando un mensaje diferente si no lo es.
   
```bash
#!/bin/bash
usuario="root"
if [ $(whoami) = $usuario ]; then
    echo "Este script no está siendo ejecutado por el usuario root"
else
    echo "Este script está siendo ejecutado por el usuario root"
fi
```

## Calificación de un examen
7. Realiza un script que pida una nota numérica y determine si es "Aprobado" (5 o más) o "Suspenso" (menos de 5).
   
```bash
#!/bin/bash
read -p "Introduce la nota del examen: " nota

if [ $nota -ge 5 ]; then
    echo "Aprobado"
else
    echo "Suspenso"
fi
```

## Comprobación del espacio en disco
8. Crea un script que compruebe el espacio libre en disco. Si el espacio es inferior al 10%, muestra un mensaje de advertencia.
   
```bash
#!/bin/bash
espacio_libre=$(df / | awk '{ print $5 }' | sed 's/%//')

if [ $espacio_libre -lt 10 ]; then
    echo "Advertencia: El espacio libre en disco es inferior al 10%"
else
    echo "El espacio libre en disco es suficiente"
fi
```

## Menú de opciones
9. Escribe un script que muestre un menú con tres opciones. El usuario debe introducir una opción y el script debe ejecutar una acción diferente dependiendo de la opción seleccionada (es suficiente con que muestre un mensaje diferente según la opción escogida)
    
```bash
#!/bin/bash
echo "Selecciona una opción:"
echo "1. Opción 1"
echo "2. Opción 2"
echo "3. Opción 3"
read -p "Introduce tu opción: " opcion

if [ $opcion -eq 1 ]; then
    echo "Has seleccionado la Opción 1"
elif [ $opcion -eq 2 ]; then
    echo "Has seleccionado la Opción 2"
elif [ $opcion -eq 3 ]; then
    echo "Has seleccionado la Opción 3"
else
    echo "Opción no válida"
fi
```

## Evaluación de edad
10. Haz un script que solicite al usuario su edad y determine si es menor, adulto o mayor de edad, según un umbral predefinido (por ejemplo, menor de 18, entre 18 y 65, y mayor de 65).
    
```bash
#!/bin/bash
read -p "Introduce tu edad: " edad

if [ $edad -lt 18 ]; then
    echo "Eres menor de edad"
elif [ $edad -le 65 ]; then
    echo "Eres adulto"
else
    echo "Eres de la tercera edad"
fi
```  

## Contar líneas de un archivo
11. Escribe un script que solicite el nombre de un archivo y luego imprima cuántas líneas tiene ese archivo. Verifica que el archivo exista antes de contar las líneas.
    
```bash
#!/bin/bash
read -p "Introduce el nombre del archivo: " archivo

if [ -f $archivo ]; then
    lineas=$(wc -l < $archivo)
    echo "El archivo tiene $lineas líneas"
else
    echo "El archivo no existe"
fi
```