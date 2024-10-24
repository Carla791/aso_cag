# Entornos multimáquina
## Pasos
1. Crea un proyecto Vagrant que genere un laboratorio para trabajar con Windows Server con las siguientes características:
    - Tendrá dos máquinas virtuales con los siguientes sistemas operativos y características:
        - Windows Server 2019 Standard
            4GB de RAM
            4 cores virtuales
        - Windows 10
            2GB de RAM
            2 cores virtualesç
Realizamos el documento vagrantfile con la siguiente información.
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


2. Las máquinas virtuales deberán estar interconectadas entre sí.
   
3. Se debe poder acceder desde equipo anfitrión a las máquinas virtuales mediante Escritorio remoto
4. Vagrant.configure("2") do |config|
  # Configuración de la máquina Windows Server 2019
  config.vm.define "windows_server" do |server|
    server.vm.box = "peru/windows-server-2019-standard"
    server.vm.network "private_network", ip: "192.168.33.10"
    server.vm.provider "virtualbox" do |vb|
      vb.memory = "4096"
      vb.cpus = 4
    end
    server.vm.provision "shell", inline: <<-SHELL
      # Habilitar Escritorio remoto en Windows Server
      Set-ItemProperty -Path 'HKLM:\\System\\CurrentControlSet\\Control\\Terminal Server' -Name "fDenyTSConnections" -Value 0
      Enable-NetFirewallRule -DisplayGroup "Remote Desktop"
    SHELL
  end

  # Configuración de la máquina Windows 10
  config.vm.define "windows_10" do |win10|
    win10.vm.box = "gusztavvargadr/windows-10"
    win10.vm.network "private_network", ip: "192.168.33.11"
    win10.vm.provider "virtualbox" do |vb|
      vb.memory = "2048"
      vb.cpus = 2
    end
    
  end
end
