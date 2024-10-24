## Pasos:
### Preparación de la máquina y configuración de la red
<!--PS D:\ASO\aso_cag\UT02_linux\practicas\PR0202> vagrant init generic/ubuntu2204 --minimal-->
<!--vagrant up-->
<!--vagrant halt-->
<!--Añadir desde virtualbox el adaptador de red solo anfitrión-->
<!--Encender la MV desde virtualbox-->
1. Indica la dirección IP que asigna VirtualBox a este adaptador de red, así como la dirección IP del adaptador correspondiente en la máquina anfitrión.
    - Dirección VirtualBox:192.168.56.1;
    - Dirección maquina anfitrion:192.168.56.1
<!--Con el comando ipconfig podremos ver la dirrecion ip -->
2.Comprueba que hay conectividad entre el anfitrión y la máquina virtual.
    - Realizamos un ping a la dirección ip
<!--Hacer ping desde la terminal a la direccion ip y desde la maquina anfitrion a la ip -->
3.Cambia el hostname de Ubuntu para que se llame {iniciales}_server. Esta operación la tienes que realizar directamente en el sistema, no mediante Vagrant.
    - sudo hostnamectl set-hostname cag_server
<!--Con el comando hostnamectl podremos comprobarlo--
<!--El hostname static no nos permite usar  "_" por lo que se queda como "cagserver" y el hostname pretty se nos queda como "cag_server"-->
<!--Con el comando hostnamectl podremos comprobarlo-->
4.Realiza los cambios necesarios en tu equipo Windows para que te resuelva localmente el nombre del servidor Ubuntu (si tienes dudas, en los recursos tienes una breve explicación de cómo hacerlo)
    - Seguimos la ruta C:\Windows\System32\drivers\etc\ y editamos el archivo hosts añadiendo la direccion ip y el hostname
<!--Desde la máquina física entramos en el explorador de archivos y seguimos esta ruta "C:\Windows\System32\drivers\etc\" y editamos el archivo hosts añadiendo la direccion ip y el hostname "192.168.56.1 cagserver"-->
<!--Como necesitamos permisos de administrador para editar el archivo lo movemos al escritorio y lo editamos, después lo movemos a donde estaba ,recordando que era un archivo sin extensión-->
### Creación del usuario y conexión SSH
1.Crea en Ubuntu un usuario que se llamará {iniciales}_ssh, donde iniciales son las de tu nombre y apellidos.
    - Sudo adduser cag_ssh(1234)
2.Realiza los pasos necesarios para que este usurio se pueda conectar mediante SSH mediante contraseña.
    - sudo mkdir /cpi
    - sudo cp /etc/ssh/sshd_config /cpi/
    - sudo nano /etc/ssh/sshd_config y añadimos #AllowUser cag_ssh
    - cat /etc/ssh/sshd_config
    - sudo /etc/init.d/ssh restart
    - ssh -p 22 cag_ssh@127.0.0.1
<!-- Utilizamos el comando cat para visualizar el fichero,y comprobar si esta modificado-->
<!--Reiniciamos el servicio ssh-->
<!--Usamos el comando ssh para conectarnos $ssh -p [PUERTO] [USUARIO]@[IP-DEL-SERVIDOR], despues introducimos yes y la contraseña(1234)-->
3.Una vez que hayas verificado que la conexión funciona haz los cambios necesarios para que la conexión se realize mediante un par de claves pública-privada de forma transparente para el usuario.
    - ssh-keygen
    - cat ~/.ssh/id_rsa.pub
    - scp ./id_rsa.pub cag_ssh@127.0.0.1:/home/cag_ssh/
<!--La clave publica se guarda en "/home/cag_ssh/.ssh/id_rsa.pub" y la clave privada en "/home/cag_ssh/.ssh/id_rsa"-->
<!--Utilizamos el comando cat para ver la clave publica en ASCII-->
<!-- -->
cat id_rsa.pub >> .ssh/authorized_keys