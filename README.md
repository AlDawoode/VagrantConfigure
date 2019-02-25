# -*- mode: ruby -*-
# vi: set ft=ruby :


Vagrant.configure("2") do |config|


  # Box Settings 
  # Operating System from https://app.vagrantup.com/boxes/search
  config.vm.box = "ubuntu/trusty64"



  # provider Settings
  # VirtualBox or another "VM"  
  config.vm.provider "virtualbox" do |vb|
    #If you want add a bit more performance to your vagrant box inside VirtualBox.
    vb.memory = 2048  #memory
    vb.cpus = 4       #processors
  end



  # Network Settings
  # How your host sees your box via browser.

  #1- The host is your localMachine and the guest is the box.
  #  config.vm.network "forwarded_port", guest: 80, host: 8080

  #2- you can use private "Local" ip address. This will not work outside of your network.
  # OBS You Can Add "HostName " instead of having to go to this ip.
  # You might want a nice "local domain"
  # You have to edit your hosts file so :
  # linux /etc/hosts
  # windows C:/windows/system32/driver/etc and you have to open notepad or something like that as administrator
  # and then open it from there and write : 192.168.33.10 AlDawoode.local www.AlDawoode.local
  # config.vm.network "private_network", ip: "192.168.33.10"

  #3- Another example for network:
  # config.vm.network "public_network"
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  
  
  
  # How you access file from your computer.
  # Folder Settings   first argument is your folder in your actual machine
  # Secound argument is which folder in your box do you want to link or sync. 
   config.vm.synced_folder ".", "/var/www/html"



  # Provision Settings
  # What we want setup 
  # You have 2 way 
  # 1- inside the vagrant file -->
   config.vm.provision "shell", inline: <<-SHELL
     apt-get update
     apt-get install -y apache2
   SHELL


 
  # or 2- outside vagrant file , you have to create bootstrap.sh file --> 
  #config.vm.provision "shell", path: "bootstrap.sh"
 



end
