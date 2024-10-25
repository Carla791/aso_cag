# Introducción a Vagrant
<!-- git init-->
## PASOS: 
1. Añadimos una imagen
    - vagrant box add {image}
<!--Seleccionamos el hipervisor: virtualbox -->
2. Crear un directorio para crear la MV y acceder a el.
   - cd UT01_introducción/practicas/PR0101 
<!--En este caso el directorio es PR0101 , ya esta creado-->
<!--El comando cd {ruta relativa}-->
3. Ver la lista de imagenes
    - vagrant box list
4. Iniciamos la MV
    - vagrant init {box} --minimal
<!--Creamos un archivo vagrantfile -->
<!--Si añadimos --minimal no nos apareceran los comentarios  en el archivo-->
5. Modificar el vatgrantfile
    - Vagrant.configure("2") do |config| 
    <!--Esta linea ya aparece-->
    - config.vm.box = "gusztavvargadr/ubuntu-server-2004-lts"
    <!--Esta linea ya aparece, nos indica el nombre de la MV que vamos a configurar -->
    - config.vm.hostname = "server-car"
    <!--Modificamos el nombre de la MV-->
    - config.vm.synced_folder "origen", "destino"
    <!--Sincronizamos un directorio de la MV con un directorio de la máquina fisica-->
    <!--origen=ruta relativa de la maquina fisica -,- "destino"=ruta absoluta al directorio en la maquina virtual-->
    - config.vm.provider "virtualbox" do |vb|
        - vb.name ="Ubuntu Server"
        <!--Modificamos el hostname de la MV-->
        - vb.memory = 2048
        <!--Modificamos la capacidad de la memoria RAM de la MV-->
        - vb.cpus= 2
        <!--Modificamos el numero de procesadores de la MV-->
    - end
    - end
    <!--Cerramos cada árbol -->
6. Creamos la carpeta que vamos a sincronizar
    - mkdir sincr
<!--utilizamos el comando mkdir-->
7. Levantar la máquina virtual
   - git init
8. Iniciar la máquina virtual
    - vagrant up
9. Acceder a la máquina virtual
    - vagrant ssh 
10.   Apagar la máquina virtual
    - vagrant halt 
11.  Realizar un seguimiento de los archivos
    - git add .
<!-- El"." añade todos los archivos del directorio en el que nos encontremos-->
12.     Enviar archivos al repositorio local
    - git commit -m "mensaje"
13.     Actualizar la información de la página github
    - git push
    
<!-- Nuestros datos se han actualizado en la página de github-->

[Volver al índice](../../index1.md)