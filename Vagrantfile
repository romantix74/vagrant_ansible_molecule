# -*- mode: ruby -*-

# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  config.vm.provider "virtualbox"
    config.vm.provider :virtualbox do |v|
    v.memory = 4096
    v.linked_clone = true
    v.cpus = 4
	config.vbguest.auto_update = false
  end

  config.vm.provision "shell", inline: <<-SHELL
    apt update -y
    apt install -y mc
	apt install -y python3-pip
	apt install -y python3-venv
	apt install -y ansible
	pip install molecule[docker]
	apt install docker.io
	usermod -a -G docker vagrant
    #if [ `ip route get 10.0.0.0/8 | wc -l` -eq 0 ]; then ip route add 10.0.0.0/8 via 10.161.0.1; fi
  SHELL

  config.vm.define "test" do |s|
    s.ssh.insert_key = false
    s.vm.synced_folder "share/", "/home/vagrant/share" #, type: "rsync"
    #create: true, group: "vagrant", owner: "vagrant"
    #s.vm.network "private_network", ip: "172.16.9.10"
    #s.vm.network "public_network", ip: "10.161.74.10", netmask:"255.255.0.0",  bridge: "ens32"
  end


end
