# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  os = "ubuntu/focal64"
  net_ip = "192.168.50"

  config.vm.define :sandbox, primary: true do |sandbox_config|
    sandbox_config.vm.provider "virtualbox" do |vb|
        vb.memory = "2048"
        vb.cpus = 1
        vb.name = "sandbox"
    end

    sandbox_config.vm.box = "#{os}"
    sandbox_config.vm.box_check_update = false
    sandbox_config.vm.host_name = 'sandbox.local'
    sandbox_config.vm.network "private_network", ip: "#{net_ip}.210"
    
    sandbox_config.vm.provision "ansible" do |ansible|
      ansible.playbook = "provisioning/playbook.yaml"
      ansible.verbose = true
      ansible.raw_arguments  = [
        "--connection=paramiko",
        "--private-key=~/.vagrant.d/insecure_private_key"
      ]
      
      
    end
    
  end

end

