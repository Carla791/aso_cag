# Ejercicios sobre los comandos `while`, `until` y `for`

## Contar hasta 10 con `for`

1. Usa un bucle for para contar del 1 al 10 e imprimir cada número en una línea nueva.

```bash
#!/bin/bash
for i in {1..10}
do
  echo $i
done
``` 

## Sumar los primeros 50 números

2. Usa `for` para sumar los primeros 50 números naturales y muestra el resultado.
 
```bash
#!/bin/bash
for i in {1..50}
do
  suma=$((suma + i))
done
echo "La suma de los primeros 50 números es: $suma"
```

## Tabla de multiplicar

3. Pide un número al usuario y usa for para imprimir su tabla de multiplicar del 1 al 10.

```bash
#!/bin/bash
read -p "Indica un número: " num
for i in {1..10}
do
  mult=$(($num * i))
  echo "$num*$i = $mult"
done
```

## Contar números pares del 1 al 20 con `while`

5. Usa while para mostrar los números pares entre 1 y 20.

```bash
#!/bin/bash
n=1
while [ $n -le 20 ]
do
  if [ $(($n % 2)) -eq 0 ]; then
     echo $n
  fi
  n=$(( $n+1 ))
done
```  

## Cuenta regresiva

7. Pide al usuario un número inicial y usa `until` para hacer una cuenta regresiva hasta llegar a cero.
   
```bash
#!/bin/bash
read -p "Indica un número: " num
until [ $num -lt 0 ]
do
  echo $num
  num=$(($num - 1))
done
```

## Imprimir solo archivos .txt

8. Usa `for` para iterar sobre todos los archivos en un directorio y mostrar solo aquellos que terminen en .txt.

```bash
#!/bin/bash
for archivo in *.txt
do
  echo $archivo
done
```

## Factorial de un número

9. Solicita un número al usuario y calcula su factorial usando un bucle for.

```bash
#!/bin/bash
read -p "Indica un número: " num
fact=1
for (( i=1; i<=$num; i++ ))
do
  fact=$(($fact * i))
done
echo "El factorial de $num es: $fact"
```

## Verificar contraseña

10. Usa `until` para pedir al usuario que ingrese una contraseña correcta, y repite hasta que la acierte.

```bash
#!/bin/bash
correcta="1234"
read -p "Indica la contraseña: " pwd
until [ $pwd = $correcta ]
do
  read -p "Indica la contraseña: " pwd
done
echo "Contraseña correcta"
```

## Adivinar un número

11. Crea un juego con while en el que el usuario intenta adivinar un número entre 1 y 10. Repite hasta que lo adivine.

```bash
#!/bin/bash
n=3
read -p "Adivina un número del 1 al 10: " num
while  [ $num != $n ]
do
  read -p "Adivina un número del 1 al 10: " num
done
echo "Has adivinado el número"
```

## Mostrar la fecha n veces

12. Pide al usuario un número n y usa for para mostrar la fecha y hora actual n veces.

```bash
#!/bin/bash
read -p "Indica un número: " num
for ((i=0;i<$num;i++))
do
  date
done
```

## Promedio de números ingresados

13. Usa while para pedir números al usuario hasta que ingrese "fin", luego muestra el promedio.
    
```bash
#!/bin/bash
cont=0
suma=0
promedio=0
read -p "Indica un número, o la palabra fin para terminar: " num
while [ $num != "fin" ]
do
  suma=$(($suma + $num))
  cont=$(($cont + 1))
  read -p "Indica un número, o la palabra fin para terminar: " num
done
if [ $cont -ne 0 ]; then
   promedio=$(($suma / $cont))
   echo "El promedio de los números es $promedio"
fi
```

## Contar palabras en una cadena

14. Pide al usuario una frase y usa for para contar y mostrar el número de palabras en ella.

```bash
#!/bin/bash
read -p "Escribe una frase: " frase

for palabra in $frase
do
  cont=$((cont + 1))
done
echo "La frase $frase tiene $cont palabras"
```

## Juego de adivinar con límites dinámicos

15. Genera un número aleatorio entre 1 y 100 y pide al usuario que adivine. Usa while y da pistas de si el número es mayor o menor, terminando cuando acierte.

```bash
#!/bin/bash
correcto=$((1+RANDOM%100))
num=0
while [ $num -ne $correcto ]
do
  read -p "Adivina un numero entre 1 y 100: " num
  if [ $num -lt $correcto ]; then
     echo "El numero correcto es mayor que $num"
  elif [ $num -gt $correcto ]; then
     echo "El numero correcto es menor que $num"
  else
     echo "El numero $num es correcto"
  fi
done
```

## Archivo con nombres de directorios

16. Usa for para listar todos los directorios en la ruta actual y escribe sus nombres en un archivo directorios.txt.

```bash
#!/bin/bash
for dir in */; do
  echo $dir >> directorios.txt
done
```

```bash
#!/bin/bash
ruta=$(pwd)

for f in *$ruta; do
  if [ -d $f ]; then
     echo $f >> directorios.txt
  fi
done
```

```bash
#!/bin/bash
ruta=$(pwd)

for f in *$ruta; do
  if [ -d $f ]; then
     echo $f >> $1.txt
  fi
done
```

<!-- $1 es para que los que escribas al lado de ./script.sh lo use de variable-->
## Generar archivos de texto numerados

17. Pide al usuario un número n y usa for para generar n archivos con nombres como archivo1.txt, archivo2.txt, etc.

```bash
#!/bin/bash
read -p "Indica un número: " num
for (( i=1; i<=$num; i++ ))
do
  touch archivo$i.txt
done
```

## Validación de entrada

19. Usa until para pedir un número entre 1 y 10. Repite hasta que el usuario ingrese un número válido en ese rango.

```bash
#!/bin/bash
num=0
read -p "Introduce un número entre 1 y 10: " num
until [ $num -ge 1 ] && [ $num -le 10 ]; do
  read -p "Introduce un número entre 1 y 10: " num
done
echo "El numero $num es válido"
```

## Script de copia de seguridad

20. Crea un script que recorra un directorio y copie todos los archivos .txt a una carpeta backup. Usa for para la iteración y if para verificar el tipo de archivo.

```bash
#!/bin/bash
ruta=$(pwd)

for fichero in $ruta/*.txt
do
  if [ -f $fichero ]; then
     cp $fichero backup/
  fi
done
```
