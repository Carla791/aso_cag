# PR0501: Carpetas personales y compartidas por un grupo

## Creación de usuarios y grupos

- Crea en tu dominio los usuarios `aperez` y `fgonzalez`.

    - Desde el Administrador del servidor seguimos la siguiente ruta:Herramientas>Active Directory Administrative Center(Centro de administración de Active Directory)>cag(local)>Users>Nuevo>Usuario>Nombre(aperez),inicio de sesion(cag\aperez),Contraseña(Villlabalter1).
  
    - Desde el Administrador del servidor seguimos la siguiente ruta:Herramientas>Active Directory Administrative Center(Centro de administración de Active Directory)>cag(local)>Users>Nuevo>Usuario>Nombre(aperez),inicio de sesion(cag\fgonzalez),Contraseña(Villlabalter1).


- Crea un grupo global denominado `alumnos` y agrega los usuarios que creaste anteriormente.
  
    - Desde el Administrador del servidor seguimos la siguiente ruta:Herramientas>Active Directory Administrative Center(Centro de administración de Active Directory)>cag(local)>Users>Nuevo>Grupo>Nombre(alumnos)>Tipo de grupo(Seguridad)>Ambito de grupo(Global)>Miembros>Agregar>(aperez),(fgonzalez)>Aceptar

## Carpetas personales

- Instala el *Administrador de recursos del servidor de archivos* que está dentro del rol *Servicios de archivos y almacenamiento*
  
    - Desde el Administrador del servidor seguimos la siguiente ruta: Administrar>Agregar roles y características>Roles de servidor>Servicios de archivos y almacenamiento>Servicios de iSCSI y archivo>Administrador de recursos del servidor de archivos>Le damos a siguiente hasta la ultima pantalla>Instalar

- Utilizando la herramienta *Servicios de archivos y de almacenamiento* del *Administrador del servidor*, crea una carpeta para cada usuario dentro de `C:\shares` y realiza los pasos necesarios para que ambos usuarios puedan ver esta carpeta como una unidad de red identificada con la letra `H:`

    - Desde el Administrador del servidor>recursos compartidos>Nuevo recurso compartido>Recurso compartidoSMB-Avanzado>Nombre(personal)>
    - Desde el Administrador del servidor seguimos la siguiente ruta:Herramientas>Usuarios y equipos de Active Directory>Selecionamos los dos usuarios>Propiedades>Perfil>Seleccionamos Carpeta particular>Selecionamos Conectar H: a: \\CAG-2019\Personal\%username%>Aceptar


- Comprueba que la carpeta de cada usuario solo pueda ser accedida por él mismo.

    - Para ello hemos de meter un Windows 10 dentro del dominio cag.local, siguiendo estos pasos:
      - Comprobar que estan en la misma red y se hacen ping
      - Crear un equipo en el servidor con el nombre del windows 10
      - Acceder al dominio con las credenciales de Administrador
      - Entramos en el dominio con un usuario(aperez)
    - Al entrar comprobamos que solo podemos acceder a nuestra carpeta


## Carpetas compartidas por un grupo

- Crea en `C:\shares` una carpeta llamada `apuntes` y realiza las tareas necesarias para que los usuarios del grupo `alumnos` puedan acceder a ella como un espacio de almacenamiento compartido.

    - Desde el Administrador del servidor>recursos compartidos>Nuevo recurso compartido>Recurso compartidoSMB-Avanzado>Nombre(apuntes)>
    - Desde el explorador de archivos vamos a la ruta C:\Shares\ >Clic derecho carpeta apuntes>Condecer acceso a>Usuarios especificos>Alumnos>Agregar>Compartir