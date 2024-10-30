# Ejercicios comando case
## Menú de operaciones matemáticas

1. Crea un script que presente un menú con las operaciones básicas (suma, resta, multiplicación, división) y solicite al usuario que elija una operación. El script debe ejecutar la operación seleccionada utilizando case.
   
```bash
#!/bin/bash
echo "Seleccione una operación:"
echo "1. Suma"
echo "2. Resta"
echo "3. Multiplicación"
echo "4. División"
read -p "Ingrese su elección (1-4): " operacion

read -p "Ingrese el primer número: " num1
read -p "Ingrese el segundo número: " num2

case $operacion in
  1) resultado=$((num1 + num2))
     echo "Resultado: $num1 + $num2 = $resultado";;
  2) resultado=$((num1 - num2))
     echo "Resultado: $num1 - $num2 = $resultado";;
  3) resultado=$((num1 * num2))
     echo "Resultado: $num1 * $num2 = $resultado";;
  4) if [ $num2 -ne 0 ]; then
       resultado=$((num1 / num2))
       echo "Resultado: $num1 / $num2 = $resultado"
     else
       echo "Error: División por cero"
     fi
     ;;
  *) echo "Opción no válida"
     ;;
esac
```

## Identificación de extensión de archivo

2. Haz un script que solicite al usuario un nombre de archivo y, usando case, determine si es un archivo de texto (.txt), un archivo comprimido (.zip o .tar.gz), o cualquier otro tipo de archivo.
   
```bash
#!/bin/bash
read -p "Ingrese el nombre del archivo: " archivo

case $archivo in
  *.txt) echo "Es un archivo de texto.";;
  *.zip) echo "Es un archivo comprimido" ;;
  *.tar.gz) echo "Es un archivo comprimido";;
  *) echo "Es otro tipo de archivo." ;;
esac
```

## Conversor de unidades

3. Crea un script que ofrezca un menú para convertir entre diferentes unidades de longitud (metros a kilómetros, pies a metros, etc.) utilizando case para gestionar las conversiones.
   
```bash
#!/bin/bash
echo "Seleccione una conversión:"
echo "1. Metros a Kilómetros"
echo "2. Pies a Metros"
echo "3. Pulgadas a Centímetros"
read -p "Ingrese su elección (1-3): " conversion
read -p "Ingrese el valor a convertir: " valor

case $conversion in
  1) resultado=$(echo "$valor / 1000" | bc -l )
     echo "$valor metros son $resultado kilómetros" ;;
  2) resultado=$(echo "$valor * 0.3048" | bc -l )
     echo "$valor pies son $resultado metros";;
  3) resultado=$(echo "$valor * 2.54" | bc -l )
     echo "$valor pulgadas son $resultado centímetros" ;;
  *) echo "Opción no válida";;
esac
```

## Menú de configuración del sistema

4. Realiza un script que presente un menú con varias opciones de configuración del sistema: por ejemplo, apagar, reiniciar o cerrar sesión. Usa case para gestionar las opciones seleccionadas.

```bash
#!/bin/bash
echo "Seleccione una opción de configuración: "
echo "1. Apagar"
echo "2. Reiniciar"
echo "3. Cerrar sesión"
read -p "Ingrese su elección (1-3): " conf

case $conf in
  1) echo "Apagando el sistema..."
     $(sudo shutdown now);;
  2) echo "Reiniciando el sistema..."
     $(sudo reboot);;
  3) echo "Cerrando sesión"
     $(skill $USER);;
  *) echo "Opción no válida";;
esac
```

## Día de la semana

5. Haz un script que solicite un número entre 1 y 7 al usuario y muestre el nombre del día correspondiente (1 para lunes, 2 para martes, etc.) utilizando case.
   
```bash
#!/bin/bash
read -p "Ingrese un número entre 1 y 7: " dia

case $dia in
  1) echo "Lunes";;
  2) echo "Martes";;
  3) echo "Miércoles";;
  4) echo "Jueves";;
  5) echo "Viernes";;
  6) echo "Sábado";;
  7) echo "Domingo";;
  *) echo "Número no válido";;
esac
```

## Clasificación de notas

6. Realiza un script que solicite una calificación numérica y, usando case, la clasifique como "Sobresaliente", "Notable", "Aprobado", o "Suspenso" según el rango de valores.

```bash
#!bin/bash

```   

## Clasificación de números
7. Haz un script que solicite un número y lo clasifique como "Positivo", "Negativo" o "Cero".
   

## Control de servicios en Linux
8. Crea un script que pregunte por el nombre de un servicio y luego presente un menú para iniciar, detener o reiniciar un servicio en Linux (como apache2 o nginx). Usa case para gestionar las opciones y los comandos correspondientes (systemctl start, stop, restart).
Después de realizar la operación solicitada comprueba su código de estado de finalización (recuerda que puedes obtener el estado de finalización de un comando con la variable $? tras ejecutarlo) y muestra un mensaje indicando si la operación se ha realizado correctamente o no.


