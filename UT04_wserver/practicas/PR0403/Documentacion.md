# PR0403: El pipeline en Powershell

### 1- El comando `Get-Date` muestra la fecha y hora actual. Muestra por pantalla únicamente el año en que estamos.
    
- `Get-Date |Format-list *`
- `Get-Date | Select-Object Year`
  
![alt](./img/Ej%201.png)

### 2- Uno de los requisitos de Windows 11 es que es procesador tenga **TPM** habilitado. Powershell dispone del comando `Get-TPM` que nos muestra información sobre este módulo. Muestra por pantalla, en formato tabla, las propiedades `TpmPresent`, `TpmReady`, `TpmEnabled` y `TpmActivated`.

- `Get-Tpm | Select-Object TmpPresent,TmpReady,TmpEnabled,TmpActivated | Format-Table`

![alt](./img/Ej%202.png)


En los siguientes ejercicios trabajaremos con los ficheros devueltos por el comando `Get-ChildItem C:\Windows\System32`.

### 3- Muestra por pantalla el número de ficheros y directorios que hay en ese directorio.

- `(Get-ChildItem C:\Windows\System32).count`
  
![alt](./img/Ej%203.png)

### 4- Los objetos devueltos por el comando anterior tienen una propiedad denominada `Extension`, que indica la extensión del archivo. Calcula el número de ficheros en el directorio que tienen la extensión `.dll`.
   
- `(Get-ChildItem C:\Windows\System32 -File | Where-Object { $_.Extension -eq ".dll" }).Count`

![alt](./img/Ej%204.png)

### 5- Muestra los ficheros del directorio con extensión `.exe` que tengan un tamaño superior a 50000 bytes.

- `Get-ChildItem C:\Windows\System32 -File | Where-Object { $_.Extension -eq ".exe" -and $_.Length -gt 50000 }`

![alt](./img/Ej%205.png)

### 6- Muestra los ficheros de este directorio que tengan extensión `.dll`, ordenados por fecha de creación y mostrando únicamente las propiedades de fecha de creación (`CreationTime`), último acceso (`LastAccessTime`) y nombre (`Name`).
   
- `Get-ChildItem C:\Windows\System32 -File | Where-Object { $_.Extension -eq ".dll" } | Sort-Object CreationTime | Select-Object CreationTime, LastAccessTime, Name`

![alt](./img/Ej%206.png)

### 7- Muestra el tamaño (`Length`) y nombre completo (`FullName`) de todos los ficheros del directorio ordenados por tamaño en sentido descendente.

- ` Get-ChildItem C:\Windows\System32 -File | Sort-Object Length -Descending  | Select-Object Length,FullName` 

![alt](./img/Ej%207.png)

### 8- Muestra el tamaño y nombre completo de todos los ficheros del directorio que tengan un tamaño superior a 10MB (10000000 bytes) ordenados por tamaño.

- `Get-ChildItem C:\Windows\System32 -File | Where-Object { $_.Length -gt 10000000  }  | Sort-Object Length -Descending  | Select-Object Length,FullName`

![alt](./img/Ej%208.png)

### 9- Muestra el tamaño y nombre completo de todos los ficheros del directorio que tengan un tamaño superior a 10MB y extensión `.exe` ordenados por tamaño.
    
- `Get-ChildItem C:\Windows\System32 -File | Where-Object { $_.Length -gt 10000000 -and $_.Extension -eq ".exe" }  | Sort-Object Length | Select-Object Length,FullName`

![alt](./img/Ej%209.png)

### 10- Muestra todos los procesos que tienen el estado `Responding` puesto a `False`, es decir, todos los procesos del sistema que se hayan colgado.

- `Get-Process | Where-Object { $_.Responding -eq $false }`

![alt](./img/Ej%2010.png)

### 11- Muestra todos los ficheros de `C:\Windows` que hayan sido creados con fecha posterior al 15 de octubre de este año.
    
- `Get-ChildItem C:\Windows -File | Where-Object { $_.CreationTime -like "15/10/2024%" }`

![alt](./img/Ej%2011.png)