# Entornos multimáquina
## Pasos
1. Crea un proyecto Vagrant que genere un laboratorio para trabajar con Windows Server con las siguientes características:
    - Tendrá dos máquinas virtuales con los siguientes sistemas operativos y características:
        - Windows Server 2019 Standard
            4GB de RAM
            4 cores virtuales
        - Windows 10
            2GB de RAM
            2 cores virtuales
Realizamos el documento vagrantfile.
<!--
 Vagrant.configure("2") do |config|
  config.vm.define "wnd10" do |m1|
    m1.vm.box = "gusztavvargadr/windows-10"
    m1.vm.network "private_network", ip: "172.19.0.4", netmask: "255.255.0.0"
    m1.vm.provider "virtualbox" do |vb|
      - vb.name =" wind10"
      - vb.memory = 2048
      - vb.cpus= 2
    end
  end   
  config.vm.define "wind-server19" do |m2|
    m2.vm.box = "gusztavvargadr/windows-server-2019-standard"
    m2.vm.network "private_network", ip: "172.19.0.5", netmask: "255.255.0.0"
    m2.vm.provider "virtualbox" do |vb|
      - vb.name =" server19"
      - vb.memory = 4096
      - vb.cpus= 4
    end
  end
end
-->

1. Las máquinas virtuales deberán estar interconectadas entre sí.
   Cuando pongo `vagrant ssh server19` o `vagrant ssh wind10` no me funciona.
   Entonces no puedo comprobar si estan interconectadas

2. Se debe poder acceder desde equipo anfitrión a las máquinas virtuales mediante Escritorio remoto
  No puedo acceder a la maquina virtual por lo que no puedo instalar el acceso remoto


[Volver al índice](../index.md)