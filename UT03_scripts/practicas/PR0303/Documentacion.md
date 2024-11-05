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

## Imprimir cada letra

4. Pide una palabra al usuario y usa `for` para imprimir cada letra en una línea nueva.

```bash
#!/bin/bash
read -p "Indica una palabra: " palabra
for i in {}

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

## Suma de dígitos

6. Pide un número al usuario y usa `while` para sumar todos sus dígitos. Por ejemplo, 123 debería devolver 6.


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

read -p "Indica un número, o la palabra fin para terminar: " num
while [ $num != "fin" ]
do
  read -p "Indica un número, o la palabra fin para terminar: " num
  suma=$((suma + $num))
  cont=$((cont++))
done
if [ $cont -ne 0 ] ; then
   promedio=$(($suma / $cont))
   echo "El promedio de los números es $promedio"
fi

```

## Contar palabras en una cadena

## Juego de adivinar con límites dinámicos

## Archivo con nombres de directorios

## Generar archivos de texto numerados

## Conteo de vocales en una cadena

## Validación de entrada

## Script de copia de seguridad

