# PR0402: Introducción a Powershell (II)

1. Visualiza las últimas cinco entradas del historial, mostrando para cada una el comando, la hora en que finalizó su ejecución y el estado de ejecución.
   
     - `Get-History -Count 5| Format-List -Property CommandLine,ExecutionStatus,EndExecutionTime`

      
    ![alt](./img/Ej%201.png)

2. Ejecuta el comando `Get-Command` (que muestra todos los comandos disponibles en Powershell) e interrúmpelo antes de que finalice su ejecución pulsando las teclas Ctrl-C. A continuación, ejecútalo dejando que finalice correctamente.

    - `Get-Command`
    - Ctrl + C
    - `Get-Command`

    ![alt](./img/Ej%202.png)

3. Vuelve a ejecutar el comando del punto 1 y comprueba las diferentes salidas de finalización de estado de ejecución.

    - `Get-History -Count 5| Format-List -Property CommandLine,ExecutionStatus,EndExecutionTime`

    ![alt](./img/EJ%203.png)


4. Muestra todos los procesos con el nombre `msedge` mostrando para cada uno el identificador, el consumo de CPU y los hilos (*threads*)

    - `Get-Process msedge | Select-Object Id,CPU,Threads`

    ![alt](./img/EJ%204.png)

5. Averigua para qué sirve el parámetro `-Delimiter` del comando `Export-CSV`

    - `Get-Help Export-Csv -online`
    - El parámetro `-Delimiter` especifica el carácter que se utiliza para separar los valores en el archivo CSV. Por ejemplo, para usar un punto y coma como delimitador
  
    ![alt](./img/Ej%205.png)

6. Muestra en una ventana la ayuda del comando `Get-History`

    - `Get-Help Get-History -ShowWindow`

    ![alt](./img/Ej%206.png)

7. Muestra un listado con todos los comandos que tengan el verbo `Update`.

    - `Get-Command -Verb update`

    ![alt](./img/Ej%207.png)


8. Ejecuta la herramienta **Recortes** y localízala usando el comando `Get-Process` teniendo en cuenta que el proceso se llama `SnippingTool.exe` 

    - `Start-Process SnippingTool.exe`
    - `Get-Process -Name SnippingTool`

    ![alt](./img/Ej%208.png)

9.  Averigua qué propiedades tienen los procesos devueltos con el comando `Get-Process`.

    - `Get-Process | Get-Member -MemberType Property`

    ![alt](./img/Ej%209.png)

10. Busca en la ayuda para qué sirve el parámetro `-MemberType` del comando `Get-Member`.

    - `Get-Help Get-Member -Online`

    ![alt](./img/Ej%2010.png)

11. Desde la línea de comandos, finaliza la ejecución de la herramienta **Recortes**.

    - `Stop-Process -Name SnippingTool`

    ![alt](./img/Ej%2011.png)

12. Muestra todos los procesos que tienen el nombre `svchost`.

    -`Get-Process -Name svchost`

    ![alt](./img/Ej%2012.png)

13. Muestra por pantalla el número de instancias del proceso `svchost`.

    - `(Get-Process -Name svchost ).count`
    
    ![alt](./img/Ej%2013.png)

14. Muestra por pantalla todos los procesos con el nombre `svchost` mostrando para cada uno: nombre, identificador, hora de inicio, tiempo total de procesador y clase de prioridad. Se deben mostrar de **forma tabular**.

    - `Get-Process -Name svchost | Select-Object Name, Id, StartTime, CPU, PriorityClass | Format-Table -AutoSize `
  
    ![alt](./img/Ej%2014%20(1).png)
    ![alt](./img/Ej%2014.png)

15. Repite la búsqueda anterior, pero ordenando por el campo tiempo total de procesador en sentido descendente.
    
    - `Get-Process -Name svchost | Select-Object Name, Id, StartTime, CPU, PriorityClass | Sort-Object CPU -Descending | Format-Table -AutoSize`
    
    ![alt](./img/Ej%2015.png)

16. Muestra los usuarios que hay en el sistema agrupándolos por la propiedad `Enabled`.
    
    - `Get-LocalUser | Group-Object -Property Enabled`
  
    ![alt](./img/Ej%2016.png)

17. Muestra los usuarios que hay en el sistema con la cuenta habilitada (propiedad `Enabled` puesta a `True`). Utiliza el filtrado con el comando `Where-Object`

    - `Get-LocalUser | Where-Object -FilterScript { $_.Enabled -eq "true" }`
  
    ![alt](./img/Ej%2017.png)

18. Muestra un listado de todos los usuarios del sistema con el nombre y la fecha de la última vez que iniciaron sesión (tienes que buscar la propiedad que indique último inicio de sesión o *last logon*)
    
    - `Get-LocalUser | Select-Object Name, LastLogon`

    ![alt](./img/Ej%2018.png)

