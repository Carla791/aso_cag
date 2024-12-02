# PR0401: Introducción a Powershell

1. Obtén ejemplos de utilización del comando `Get-LocalUser`.
   
   - `Get-LocalUser`
   - `Get-LocalUser -Name Administrador`
   - `Get-LocalUser -SID S-1-5-21-1953113394-851750987-2007909317-500`
  
    ![alt](./img/Ej%201.png)

2. Obtén un listado de todos los comandos relacionados con la gestión de usuarios locales (es decir, con el nombre `LocalUser`).

    - `Get-Command -Name *LocalUser*`    

    ![alt](./img/Ej%202.png)

3. Utilizando la línea de comandos, muestra en el navegador la ayuda del comando `Get-LocalUser`.

   - `Get-Help Get-LocalUser -Online`   
    
   ![alt](./img/Ej%203%20(1).png)
   ![alt](./img/Ej%203%20(2).png)

4. Averigua para qué sirve el comando `Set-Content` y explícalo brevemente con tus palabras.

   - El comando `Set-Content` se utiliza para escribir contenido nuevo o reemplazar el contenido existente en un archivo. A diferencia de `Add-Content`, que agrega contenido al final del archivo, `Set-Content` sobrescribe el contenido existente.

5. Explica tres formas diferentes de ver o buscar un comando que hayas utilizado anteriormente en tu sesión.
    - `Get-Command`
    - `Get-History`
    - Ctrl+R 

    ![alt](./img/ej%205.png)
    ![alt](./img/Ej%205%20(1).png)
    ![alt](./img/Ej%205%20(3).png)

6. Averigua si el comando `Get-Process` tienen un parámetro llamado `ComputerName` y en caso afirmativo explica para qué sirve.
   
   - `Get-Help Get-Process -Online`
   - El parámetro `ComputerName` en el comando `Get-Process` se utilizaba para especificar el nombre de un equipo remoto desde el cual se deseaba obtener la lista de procesos.

   ![alt](./img/Ej%206.png)

7. Muestra la ayuda del comando `Start-Process` en una ventana emergente.

   - `Get-Help Start-Process -ShowWindow`

   ![alt](./img/Ej%207.png)

8. Muestra la ayuda del comando `Get-Help` en el navegador invocándolo desde la línea de comandos.
   
    - `Get-Help Get-Help -Online`
  
    ![alt](./img/EJ%208%20(1).png)
    ![alt](./img/EJ%208%20(2).png)

9.  Muestra las últimas 20 entradas del historial.

    - `Get-History -Count 20`

    ![alt](./img/Ej%209.png)

10. Elimina las entradas 10, 12 y 14 de tu historial.

    - `Clear-History -Id 10,12,14`
  
    ![alt](./img/Ej%2010.png)