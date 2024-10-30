## Pasos:
### Preparación de la máquina y configuración de la red
<!--PS D:\ASO\aso_cag\UT02_linux\practicas\PR0202> vagrant init generic/ubuntu2204 --minimal-->
<!--vagrant up-->
<!--vagrant halt-->
<!--Añadir desde virtualbox el adaptador de red solo anfitrión-->
<!--Encender la MV desde virtualbox, sino no funcionara-->
1. Indica la dirección IP que asigna VirtualBox a este adaptador de red, así como la dirección IP del adaptador correspondiente en la máquina anfitrión.
    - Utilizamos el comando `ip address` y nos aparece el adaptor que añadimos pero no hay asignada ninguna IP.
    - Editamos el archivo /etc/netplan/01-network-manager-all.yaml y le añadimos esta linea :`eth1: dhcp4: true`
    - Aplicamos la configuración con `sudo netplan apply`
2. Comprueba que hay conectividad entre el anfitrión y la máquina virtual.
   - Realizamos un ping de la máquina física a la máquina virtual
   - Realizamos un ping de la máquina virtual a la máquina física
  
3. Cambia el hostname de Ubuntu para que se llame {iniciales}_server. Esta operación la tienes que realizar directamente en el sistema, no mediante Vagrant.
    - Cambiar el hostanme con el comando`sudo hostnamectl set-hostname cag_server`
<!--Con el comando hostnamectl podremos comprobarlo-->
<!--El hostname static no nos permite usar  "_" por lo que se queda como "cagserver" y el hostname pretty se nos queda como "cag_server"-->
<!--Con el comando hostnamectl podremos comprobarlo-->
4. Realiza los cambios necesarios en tu equipo Windows para que te resuelva localmente el nombre del servidor Ubuntu 
    - Seguimos la ruta C:\Windows\System32\drivers\etc\ y editamos el archivo hosts añadiendo la direccion ip y el hostname
    - Comprobación:`ping cagserver`
<!--Desde la máquina física entramos en el explorador de archivos y seguimos esta ruta "C:\Windows\System32\drivers\etc\" y editamos el archivo hosts añadiendo la direccion ip y el hostname "192.168.56.1 cagserver"-->
<!--Como necesitamos permisos de administrador para editar el archivo lo movemos al escritorio y lo editamos, después lo movemos a donde estaba ,recordando que era un archivo sin extensión-->

### Creación del usuario y conexión SSH
1. Crea en Ubuntu un usuario que se llamará {iniciales}_ssh, donde iniciales son las de tu nombre y apellidos.
    - Crear el usuario con el comando `Sudo adduser cag_ssh` contraseña= 1234
2. Realiza los pasos necesarios para que este usurio se pueda conectar mediante SSH mediante contraseña.
    - Instalamos el paquete ssh `sudo apt-get install openssh-server`
    - Modificamos el archivo sshd_config con `sudo nano /etc/ssh/sshd_config` y añadimos la línea `#AllowUser cag_ssh`
    - Reseteamos el servicio con el comando `sudo /etc/init.d/ssh restart`
    - Nos conectamos mediante ssh `ssh cag_ssh@carlaserver`
<!-- Utilizamos el comando cat para visualizar el fichero,y comprobar si esta modificado-->
<!--Reiniciamos el servicio ssh-->
<!--Usamos el comando ssh para conectarnos $ssh -p [PUERTO] [USUARIO]@[IP-DEL-SERVIDOR], despues introducimos yes y la contraseña(1234)-->
3. Una vez que hayas verificado que la conexión funciona haz los cambios necesarios para que la conexión se realize mediante un par de claves pública-privada de forma transparente para el usuario.
    - Creamos un par de claves publica-privada `ssh-keygen`
    - cat ~/.ssh/id_rsa.pub
    - Mandamos la clave pública al servidor con el comando`scp ./id_rsa.pub cag_ssh@carlaserver:/home/cag_ssh/`
    - Copiaremos la clave pública desde el cliente al fichero `~/.ssh/authorized_keys` con el comando `cat id_rsa.pub >> .ssh/authorized_keys`
    - YA no nos pedira la contraseña al conectarnos.
<!--La clave publica se guarda en "/home/cag_ssh/.ssh/id_rsa.pub" y la clave privada en "/home/cag_ssh/.ssh/id_rsa"-->
<!--Utilizamos el comando cat para ver la clave publica en ASCII-->
<!--Con el comando scp mandamos la clave al servidor-->
<!--Comprobamos con ls que se ha enviado la clave-->

### Conexión transparente a Github
1. Ahora que ya estás cómodo con la autenticación mediante par de claves pública-privada, intenta configurar tu Github para que te puedas conectar sin necesidad de introducir tu contraseña. Como pista, tienes que acceder a tu perfil -> Settings -> SSH and GPG keys
    - Generamos un par de claves formato ed25519 para github conectada al correo de github con el comando `ssh-keygen -t ed25519 -C "carla.alvgar@educa.jcyl.es"`
    - Copiamos la clave pública para incluirla en los ajustes de la cuenta de github con el comando `ssh-ed25519 "clave pública" carla.alvgar@educa.jcyl.es`
    - Iniciar ssh  con el comando `Start-Service ssh-agent` 
    - Agregar la clave privada a ssh `ssh-add C:\Users\Alumno\.ssh\id_ed25519`
    - Establecer conexión con github mediante ssh `ssh -T git@github.com`
<!--La clave publica se guarda en "C:\Users\Alumno/.ssh/id_ed25519.pub" y la clave privada en "C:\Users\Alumno/.ssh/id_ed25519"-->
