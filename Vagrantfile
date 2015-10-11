# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "boxcutter/centos64-i386"
  config.ssh.insert_key = false
  config.vm.boot_timeout = 300
  config.vm.post_up_message = "Welcome to the Ansibles CentOS 6 development environment."
  config.vm.provider :virtualbox do |v|
    v.name = "example"
    v.memory = 512
    v.cpus = 2
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end
  config.vm.network "private_network", ip: "192.168.33.33"
  config.vm.network :forwarded_port, guest: 80, host: 8888
  config.vm.network :forwarded_port, guest: 3306, host: 3306
  config.vm.define :example do |example|
  end
  config.vm.hostname = "example"
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/example-site.yml"
    ansible.inventory_path = "provisioning/inventory"
    ansible.sudo = true
  end
end