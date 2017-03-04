# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.ssh.insert_key = false
  config.vm.define :centos_nginx do |web|
    web.vm.box = "Centos64"
    web.vm.network :private_network, ip: "192.168.33.12"
    web.vm.network "public_network", bridge: "enp5s0" , ip: "192.168.131.128"
    web.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512","--cpus", "1", "--name", "centos-nginx" ]
    end
    config.vm.provision :chef_solo do |chef|
      chef.cookbooks_path = "cookbooks"
      chef.add_recipe "nginx"
    end
  end
  config.vm.define :centos_web1 do |web|
    web.vm.box = "Centos64_updated"
    web.vm.network :private_network, ip: "192.168.33.13"
    web.vm.network "public_network", bridge: "enp5s0" , ip: "192.168.131.127"
    web.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512","--cpus", "1", "--name", "centos-web1" ]
    end
    config.vm.provision :chef_solo do |chef|
      chef.cookbooks_path = "cookbooks"
      chef.add_recipe "web"
      chef.json ={"web" => {"idServer" => "1"}}
    end
  end
  config.vm.define :centos_web2 do |web|
    web.vm.box = "Centos64_updated"
    web.vm.network :private_network, ip: "192.168.33.14"
    web.vm.network "public_network", bridge: "enp5s0" , ip: "192.168.131.126"
    web.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512","--cpus", "1", "--name", "centos-web2" ]
    end
    config.vm.provision :chef_solo do |chef|
      chef.cookbooks_path = "cookbooks"
      chef.add_recipe "web"
      chef.json ={"web" => {"idServer" => "2"}}
    end
  end
  config.vm.define :centos_db do |db|
    db.vm.box = "Centos64_updated"
    db.vm.network :private_network, ip: "192.168.33.15"
    db.vm.network "public_network", bridge: "enp5s0" , ip: "192.168.131.125"
    db.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "512","--cpus", "1", "--name", "centos-db" ]
    end
    config.vm.provision :chef_solo do |chef|
      chef.cookbooks_path = "cookbooks"
      chef.add_recipe "db"
    end
  end  
end
