## Pasos:
### Entorno de trabajo
Usaremos el box denominado generic/ubuntu2204. Tendremos que agregar un adaptador en modo puente.
<!--PS D:\ASO\aso_cag\UT02_linux\practicas\PR0202> vagrant init generic/ubuntu2204 --minimal-->
<!--vagrant up-->
<!--vagrant halt-->
<!--Añadir desde virtualbox el adaptador de red modo puente e iniciar la MV desacoplada-->
<!-- vagrant ssh-->
<!--ip address-->
### Preparación de la máquina y configuración de la red
1. Ponte de acuerdo con tus compañeros con la dirección de red que vais a utilizar y la IP asignada a cada equipo. Para evitar colisiones con la red del centro utiliza una red privada de clase B.
    - Modificamos el fichero "/etc/netplan/00-installer-config.yaml" y añadimos la ip acordada con la máscara
      - cd /etc/netplan
      - sudo nano 00-installer-config.yaml
        <!--# This is the network config written by 'subiquity'
        network:
        ethernets:
            eth0:
            dhcp4: true
            dhcp6: false
            eth1:
            addresses: [172.21.1.2/16]
        version: 2-->
        <!--Llamamos eth1 a la red puente y le añadimos la direccion -->
    - Actualizamos el servicio de red
      - sudo netplan apply
        <!--Para que ejecute los nuevos cambios-->
      - ip address 
        <!--Comprobar que se realizaron los cambios -->
    - Hacer ping al compañero 
    <!--Hacemos ping para ver si establecen comunicación -->
2. En tu servidor crea una cuenta de usuario para tí y otra para cada uno de tus compañeros
   - Creamos nuestro usuario
        - sudo adduser carla
        <!--contraseña "1234" -->
   - Creamos el usuario para nuestro compañero
        - sudo adduser alvaro
        <!--contraseña "1234" -->
3. Realiza los pasos necesarios para que tus compañeros se puedan conectar de forma transparente desde su servidor al tuyo.
    - Crear las claves publica y privada
      - ssh-keygen
      - cat ~/.ssh/id_rsa.pub
      - scp ~/.ssh/id_rsa.pub carla@172.21.1.3:/home/carla/
  <!--La clave publica se guarda en "/home/carla/.ssh/id_rsa.pub" y la clave privada en "/home/carla/.ssh/id_rsa"-->
  <!--Utilizamos el comando cat para ver la clave publica en ASCII-->
  <!--El comando scp comparte la clave publica en el servidor-->
    - Acceder a través de ssh al ordenador del compañero
      - ssh carla@172.21.1.3 
      - exit
      - ssh carla@172.21.1.3
  <!--contraseña "Villabalter1" y solo nos hara falta la primera vez, después ya no nos la pedirá-->
  <!-- -->

