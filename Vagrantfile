# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  # config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.network "public_network"
  config.vm.synced_folder "./share", "/mnt/share", create: true
  config.vm.synced_folder "./www", "/var/www", create: true

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = '/mnt/share/ansible/site.yml'
    ansible.verbose = true
    ansible.install = true
    ansible.limit = 'all'
    ansible.inventory_path = '/mnt/share/ansible/inventories/test/hosts'
  end
  config.vm.provision "shell", run: "always", inline: <<-SHELL
    ip addr | grep 'inet ' | awk '{ print $2 }'
  SHELL

end
