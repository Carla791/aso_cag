# Redes en Vagrant 
<!-- git init-->
## PASOS: 
1. Añadimos una imagen
    - vagrant box add {image}
<!--Seleccionamos el hipervisor: virtualbox -->
2. Crear un directorio para crear la MV y acceder a el.
   - cd UT01_introducción/practicas/PR0103 
<!--En este caso el directorio es PR0103 , ya esta creado-->
<!--El comando cd {ruta relativa}-->
3. Ver la lista de imagenes
    - vagrant box list
4. Iniciamos la MV
    - vagrant init {box} --minimal
<!--Crea un archivo vagrantfile -->
<!--Si añadimos --minimal no nos apareceran los comentarios  en el archivo-->
5. Modificar el vagrantfile
    - Vagrant.configure("2") do |config| 
    <!--Esta linea ya aparece-->
    - config.vm.box = "bento/ubuntu-20.04"
    <!--Esta linea ya aparece, nos indica el nombre de la MV que vamos a configurar -->
    - config.vm.hostname = "web-car"
    <!--Modificamos el hostname-->
    - config.vm.synced_folder "origen", "destino"
    <!--Sincronizamos un directorio de la MV con un directorio de la máquina fisica-->
    <!--origen=ruta relativa de la maquina fisica     "destino"=ruta absoluta al directorio en la maquina virtual-->
    - config.vm.network "forwarded_port", guest: 80, host: 8080
    <!--Realizamos una redirección de puertos-->
    <!--Redirige un puerto de la MV a otro puerto de la máquina física-->
    - config.vm.network "private_network", ip: "172.16.0.0"
    <!--Añade un adaptador de red privada-->
    - config.vm.network "public_network", ip: "10.99.0.0"
    <!--Añade un adaptador de red pública-->
    - config.vm.provider "virtualbox" do |vb|
        - vb.name ="Ubuntu Server"
        <!--Modificamos el nombre de la MV-->
        - vb.memory = 2048
        <!--Modificamos la capacidad de la memoria RAM de la MV-->
        - vb.cpus= 2
        <!--Modificamos el numero de procesadores de la MV-->
    - end
    - end
    <!--Cerramos cada árbol -->
6. Levantar la máquina virtual
    - vagrant up  
7. Acceder a la máquina virtual
    - vagrant ssh 
8. Instalar un servidor Apache
    - sudo apt-get install apache2
  <!--Si buscamos desde la máquina fisica localhost:8080 nos saldra la pagina del servidor apache-->
9. Creamos un html enlazado a otros dos archivos html
  <!-- Lo creamos en la carpeta que hemos enlazado-->
  <!-- Al buscar localhost:8080 nos saldrá nuestra pagina html-->
10.  Sacar la captura de pantalla de la pagina web.
11.   Realizar un seguimiento de los archivos
    - git add .
<!-- El"." añade todos los archivos del directorio en el que nos encontremos-->
12.     Enviar archivos al repositorio local
    - git commit -m "mensaje"
13.     Actualizar la información de la página github
    - git push
<!-- Nuestros datos se han actualizado en la página de github-->
  <!-- -->
  

  [Volver al índice](../index.md)