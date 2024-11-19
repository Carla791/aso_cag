# Proyecto ASO de la 1ª Evaluación

## Descripción del Proyecto

Este proyecto consiste en un script en Bash que permite realizar un análisis de red en un rango de direcciones IP especificado por el usuario en formato CIDR. El script identifica equipos activos en la red, determina el sistema operativo de cada uno y escanea puertos abiertos para identificar servicios en ejecución. La información recopilada se guarda en un archivo de salida, lo que facilita su revisión posterior.

## Funcionalidades del Script

### Obtención del Servicio a partir del Puerto:

- Funcionalidad: La función get_service busca el nombre del servicio asociado a un puerto dado utilizando un archivo CSV (tcp.csv).

- Implementación: Utiliza awk para filtrar el archivo y extraer el nombre del servicio, eliminando comillas innecesarias.

```bash
function get_service() {
    local port=$1
    awk -F, -v port="$port" 'NR > 1 && $2 == port {gsub(/"/, "", $3); print $3}' ./puertos/tcp.csv
}
``` 

### Función para Obtener la Dirección MAC:
- Funcionalidad: La función get_mac obtiene la dirección MAC asociada a una dirección IP específica utilizando el comando arp.

- Implementación: Ejecuta el comando arp -n para listar las direcciones IP y sus correspondientes direcciones MAC. Utiliza awk para filtrar la salida, imprimiendo solo la dirección MAC de la IP solicitada, ignorando la primera línea de la salida.

```bash
function get_mac() {
    local ip=$1
    arp -n "$ip" | awk 'NR > 1 {print $3}'
}
```

### Función para Generar Salida en Formato CSV:
- Funcionalidad: La función output_csv genera un archivo de salida en formato CSV que contiene la información recopilada durante el análisis de red, incluyendo direcciones IP, direcciones MAC, sistemas operativos y puertos abiertos.

- Implementación: Inicializa el archivo CSV escribiendo un encabezado que describe las columnas. Luego, itera sobre un array results que contiene las entradas recopiladas, escribiendo cada entrada en el archivo de salida.

```bash
function output_csv() {
    local output_file=$1
    echo "IP,MAC,OS,Open Ports" > "$output_file"
    for entry in "${results[@]}"; do
        echo "$entry" >> "$output_file"
    done
}
```

### Entrada de Dirección IP en Formato CIDR:

- Funcionalidad: Solicita al usuario que introduzca una dirección IP en formato CIDR (por ejemplo, 192.168.1.0/24).

- Implementación: Se utiliza read para capturar la entrada del usuario y IFS para separar la dirección de red y la máscara.

```bash
read -p "Introduce la dirección IP en formato CIDR (ej. 192.168.1.0/24): " cidr
IFS='/' read -r network mask <<< "$cidr"
```

### Cálculo del Rango de IPs basado en la máscara:

- Funcionalidad: Calcula el rango de direcciones IP que se pueden escanear en función de la máscara proporcionada.

- Implementación: Se utiliza un case para determinar el rango basado en la máscara.

```bash
case $mask in
    1)  range=256 ;;
    2)  range=65536 ;;
    3)  range=16777216 ;;
    *)  echo "Máscara no soportada. Debe ser /8, /16 o /24." ; exit 1 ;;
esac
```

### Inicializar el Archivo de Salida:
-Funcionalidad: Esta parte del script inicializa un archivo de salida donde se almacenará la información recopilada durante el análisis de red.

- Implementación: Utiliza el comando echo para escribir un encabezado en el archivo que indica que se trata de un análisis de red para la dirección CIDR especificada por el usuario. También se añade una línea de separación para mejorar la legibilidad del archivo.

```bash
echo "Análisis de red para $cidr" > "$output_file"
echo "===================================" >> "$output_file"
``` 

### Registrar la Marca de Tiempo de Inicio:
- Funcionalidad: Se registra la marca de tiempo de inicio del análisis para poder medir la duración del proceso posteriormente.

- Implementación: Utiliza el comando date con el formato %s, que devuelve el tiempo actual en segundos desde la época (1 de enero de 1970). Este valor se almacena en la variable start_time.

```bash
start_time=$(date +%s)
``` 

### Escaneo de la Red:

- Funcionalidad: Escanea las direcciones IP en el rango especificado, enviando pings para identificar equipos activos.

- Implementación: Utiliza un bucle for junto con ping para comprobar la disponibilidad de cada IP.

```bash
echo "Escaneando la red..."
for i in $(seq 1 $((range - 2))); do
    ip="${network%.*}.$i"
    if ping -c 1 -W 1 "$ip" &> /dev/null; then
        echo "Equipo encontrado: $ip"
        echo "Equipo encontrado: $ip" >> "$output_file"
    fi
done
```

### Obtener Dirección MAC:
- Funcionalidad: Esta parte del script obtiene la dirección MAC asociada a una dirección IP específica y la muestra en la consola.

- Implementación: Llama a la función get_mac pasando la dirección IP como argumento y almacena el resultado en la variable mac. Luego, utiliza el comando echo para imprimir la dirección MAC en la consola y también la registra en el archivo de salida, asegurando que la información esté disponible tanto para el usuario como para la documentación del análisis.

```bash
mac=$(get_mac "$ip")
echo "MAC del equipo: $mac"
echo "MAC del equipo: $mac" >> "$output_file"
```

### Detección del Sistema Operativo basado en TTL:

- Funcionalidad: Determina el sistema operativo de cada equipo activo basado en el valor TTL de la respuesta del ping.

- Implementación: Se extrae el TTL y se compara con valores conocidos para Linux y Windows.

```bash
ttl=$(ping -c 1 "$ip" | grep "ttl=" | awk -F'ttl=' '{print $2}' | awk '{print $1}')
if [[ $ttl -eq 63 ]]; then
    os="Linux"
elif [[ $ttl -eq 127 ]]; then
    os="Windows"
else
    os="Desconocido"
fi
echo "Sistema operativo: $os"
echo "Sistema operativo: $os" >> "$output_file"
```

### Escaneo de Puertos Abiertos:

- Funcionalidad: Escanea los puertos del 1 al 1024 para identificar cuáles están abiertos y qué servicios están corriendo.
  
- Implementación: Utiliza nc (netcat) para escanear puertos y llama a la función get_service para identificar el servicio asociado a cada puerto abierto.

```bash
echo "Escaneando puertos abiertos en $ip..."
for port in {1..1024}; do
    if nc -z -w 1 "$ip" "$port" 2>/dev/null; then
        service=$(get_service "$port")
        service=${service:-"Desconocido"}
        echo "Puerto abierto: $port (Servicio: $service)"
        echo "Puerto abierto: $port (Servicio: $service)" >> "$output_file"
    fi
done
```

### Registrar la Marca de Tiempo de Finalización:
- Funcionalidad: Se registra la marca de tiempo de finalización del análisis para poder calcular el tiempo total que tomó el proceso.

- Implementación: Similar a la marca de tiempo de inicio, se utiliza el comando date con el formato %s para obtener el tiempo actual en segundos desde la época. Este valor se almacena en la variable end_time. Luego, se calcula el tiempo transcurrido restando start_time de end_time, y el resultado se almacena en la variable elapsed_time.

```bash
end_time=$(date +%s)
elapsed_time=$((end_time - start_time))
```

### Registro de Resultados:

- Funcionalidad: Guarda todos los resultados del análisis en un archivo especificado por el usuario, incluyendo la dirección IP, el sistema operativo detectado y los puertos abiertos.

- Implementación: Se inicializa un archivo de salida y se escribe en él durante el escaneo.

```bash
echo "Análisis completado. La información se ha guardado en $output_file."
echo "Tiempo total de ejecución: $elapsed_time segundos."
echo "Tiempo total de ejecución: $elapsed_time segundos." >> "$output_file"
```
## Script completo 
```bash
#!/bin/bash

# Función para obtener el servicio a partir del puerto
function get_service() {
    local port=$1
    awk -F, -v port="$port" 'NR > 1 && $2 == port {gsub(/"/, "", $3); print $3}' ./puertos/tcp.csv
}

# Función para obtener la dirección MAC
function get_mac() {
    local ip=$1
    arp -n "$ip" | awk 'NR >1 {print $3}'
}

# Función para generar salida en formato CSV
function output_csv() {
    local output_file=$1
    echo "IP,MAC,OS,Open Ports" > "$output_file"
    for entry in "${results[@]}"; do
        echo "$entry" >> "$output_file"
    done
}

# Solicitar la dirección IP en formato CIDR
read -p "Introduce la dirección IP en formato CIDR (ej. 192.168.1.0/24): " cidr

# Extraer la red y la máscara
IFS='/' read -r network mask <<< "$cidr"

# Calcular el rango de IPs basado en la máscara
case $mask in
    24) range=256 ;;
    16) range=65536 ;;
    8)  range=16777216 ;;
    *)  echo "Máscara no soportada. Debe ser /8, /16 o /24." ; exit 1 ;;
esac

# Archivo de salida
read -p "Introduce el nombre del archivo para guardar la información: " output_file

# Inicializar el archivo de salida
echo "Análisis de red para $cidr" > "$output_file"
echo "===================================" >> "$output_file"

# Registrar la marca de tiempo de inicio
start_time=$(date +%s)

# Escaneo de red
echo "Escaneando la red..."
for i in $(seq 1 $((range - 2))); do
    ip="${network%.*}.$i"
    if ping -c 1 -W 1 "$ip" &> /dev/null; then
        echo "Equipo encontrado: $ip"
        echo "Equipo encontrado: $ip" >> "$output_file"
# Obtener dirección MAC
mac=$(get_mac "$ip")
echo "MAC del equipo:$mac"
echo "MAC del equipo:$mac" >> "$output_file"

# Detección del sistema operativo basado en TTL
ttl=$(ping -c 1 "$ip" | grep "ttl=" | awk -F'ttl=' '{print $2}' | awk '{print $1}')
if [[ $ttl -eq 64 ]]; then
   os="Linux"
elif [[ $ttl -eq 128 ]]; then
   os="Windows"
else
   os="Desconocido"
fi
echo "Sistema operativo: $os"
echo "Sistema operativo: $os" >> "$output_file"

        # Detección de puertos abiertos
        echo "Escaneando puertos abiertos en $ip..."
        for port in {1..1024}; do
            if nc -z -w 1 "$ip" "$port" 2>/dev/null; then
                service=$(get_service "$port")
                service=${service:-"Desconocido"}
                echo "Puerto abierto: $port (Servicio: $service)"
                echo "Puerto abierto: $port (Servicio: $service)" >> "$output_file"
            fi
        done
        echo "-----------------------------------" >> "$output_file"
    fi
done

# Registrar la marca de tiempo de finalización
end_time=$(date +%s)
elapsed_time=$((end_time - start_time))

echo "Análisis completado. La información se ha guardado en $output_file."
echo "Tiempo total de ejecución: $elapsed_time segundos."
echo "Tiempo total de ejecución: $elapsed_time segundos." >> "$output_file"
```

## Ejemplo de prueba
```bash
vagrant@ubuntu2204:~$ cat final.txt
Análisis de red para 10.0.2.0/24
===================================
Equipo encontrado: 10.0.2.2
MAC del equipo:52:54:00:12:35:02
Sistema operativo: Linux
Puerto abierto: 135 (Servicio: DCE endpoint resolution)
Puerto abierto: 443 (Servicio: HTTP protocol over TLS/SSL)
Puerto abierto: 445 (Servicio: Microsoft-DS)
Puerto abierto: 623 (Servicio: Aux Bus Shunt)
Puerto abierto: 902 (Servicio: VMware Authentication Daemon / IDEAFARM-CHAT)
Puerto abierto: 912 (Servicio: VMware Authentication Daemon)
-----------------------------------
Equipo encontrado: 10.0.2.3
MAC del equipo:52:54:00:12:35:03
Sistema operativo: Linux
Puerto abierto: 53 (Servicio: Domain Name Server)
Puerto abierto: 135 (Servicio: DCE endpoint resolution)
Puerto abierto: 443 (Servicio: HTTP protocol over TLS/SSL)
Puerto abierto: 445 (Servicio: Microsoft-DS)
Puerto abierto: 623 (Servicio: Aux Bus Shunt)
Puerto abierto: 902 (Servicio: VMware Authentication Daemon / IDEAFARM-CHAT)
Puerto abierto: 912 (Servicio: VMware Authentication Daemon)
-----------------------------------
Equipo encontrado: 10.0.2.4
MAC del equipo:52:54:00:12:35:04
Sistema operativo: Linux
Puerto abierto: 135 (Servicio: DCE endpoint resolution)
Puerto abierto: 443 (Servicio: HTTP protocol over TLS/SSL)
Puerto abierto: 445 (Servicio: Microsoft-DS)
Puerto abierto: 623 (Servicio: Aux Bus Shunt)
Puerto abierto: 902 (Servicio: VMware Authentication Daemon / IDEAFARM-CHAT)
Puerto abierto: 912 (Servicio: VMware Authentication Daemon)
-----------------------------------
Equipo encontrado: 10.0.2.15
MAC del equipo:
Sistema operativo: Linux
Puerto abierto: 22 (Servicio: SSH Remote Login Protocol)
-----------------------------------
Tiempo total de ejecución: 3346 segundos.
```