# -*- mode: ruby --
# vi: set ft=ruby :
require "yaml"

# Load in external config
config_file = "#{File.dirname(__FILE__)}/vm_config.yml"
default_config_file = "#{File.dirname(__FILE__)}/.vm_config_default.yml"

if !File.file? config_file
  puts "Creating vm_config.yml..."
  FileUtils.cp default_config_file, config_file
end

vm_external_config = YAML.load_file(config_file)

# Install ansible modules
system "ansible-galaxy install -r requirements.yml"

Vagrant.configure(2) do |config|
  config.vm.box = "geerlingguy/ubuntu1404"

  config.vm.synced_folder vm_external_config["lybrary_path"], "/home/vagrant/code/Lybrary", :nfs => true

  config.vm.provider :virtualbox do |v|
    v.name = "imagesServer"
    v.memory = vm_external_config["memory"]
    v.cpus = 2
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--ioapic", "on"]
  end

  config.vm.hostname = "team"
  config.vm.network :private_network, ip: vm_external_config["ip"]

  # Set the name of the VM. See: http://stackoverflow.com/a/17864388/100134
  config.vm.define :team do |team|
  end

  # Ansible provisioner.
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    ansible.inventory_path = "provisioning/inventory"
    ansible.sudo = true
  end
end
