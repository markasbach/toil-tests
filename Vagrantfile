# -*- mode: ruby -*-
# vi: set ft=ruby :

# define VMs to run toil tests on
Vagrant.configure("2") do |config|

  # pass-through authentication: allows the vagrant machines to use keys from the master -- very useful for source code checkouts
  config.ssh.forward_agent = true

  # disallow creation of symbolic links inside the shared folder from within the virtual machines
  config.vm.synced_folder '.', '/vagrant', SharedFoldersEnableSymlinksCreate: false
  
  # get enough RAM and two CPUs so we can test parallelism
  config.vm.provider "virtualbox" do |virtualbox|
      virtualbox.memory = "4096"
      virtualbox.cpus = "2"
  end

  # let ansible do the setup of all machines
  config.vm.provision "ansible" do |ansible|
    ansible.compatibility_mode = "2.0"
    ansible.playbook = "toil.yml"
    ansible.extra_vars = { ansible_python_interpreter:"/usr/bin/python3" }
  end

  # stock Ubuntu 18.04 (has python 3.6)
  config.vm.define "bionic", autostart: false do |bionic|
    bionic.vm.box = "ubuntu/bionic64"
    bionic.vm.hostname = "bionic"
  end

  # stock Ubuntu 16.04 (has python 3.5)
  config.vm.define "xenial", autostart: false do |xenial|
    xenial.vm.box = "ubuntu/xenial64"
    xenial.vm.hostname = "xenial"
  end
end
