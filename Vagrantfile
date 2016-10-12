#-*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.provider :virtualbox do |vb|
    vb.customize ["modifyvm", :id, "--memory", "4096"]
  end

# vtechworks server

  config.vm.define "vtechworksvm" do |vtechworksvm|
    vtechworksvm.vm.hostname = "vtechworksvm"
    vtechworksvm.vm.box = "ubuntu/trusty64"
    vtechworksvm.vm.network :private_network, ip: "192.168.60.4"
    vtechworksvm.vm.synced_folder "dspace/dspace/target/dspace-installer", "/var/local/vtechworks/src/dspace/dspace/target/dspace-installer", type: "rsync"
      end
# customizations to forward host git settings
  config.ssh.insert_key = false

# Ansible provision

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/site.yml"
  end
end
