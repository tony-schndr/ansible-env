# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "bento/ubuntu-20.04"
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true

  config.vm.provider :virtualbox do |v|
    v.name = "ansible"
    v.memory = 8192
    v.cpus = 2
    # v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    # v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  config.vm.hostname = "ansible"
  config.vm.network :private_network, ip: "192.168.33.55"

  # Set the name of the VM. See: http://stackoverflow.com/a/17864388/100134
  config.vm.define :ansible do |ansible|
  end

  # Ansible provisioner.
  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "datapower.yml"
    ansible.inventory_path = "inventory"
    ansible.become = true
  end

end
