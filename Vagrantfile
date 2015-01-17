# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.

  # default is a small vm
  config.vm.box = "ubuntu-trusty"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"
  config.vm.provider "virtualbox" do |v|
    v.memory = 512
    v.cpus = 1
  end
  config.ssh.insert_key = false

  config.vm.define "webapp" do |webapp_config|
    webapp_config.vm.hostname = "web"
    webapp_config.vm.network :private_network, ip: "172.16.0.10", :netmask => "255.255.255.0"
    webapp_config.vm.provider "virtualbox" do |v|
      v.memory = 512
      v.cpus = 1
    end
  end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = 'site.yml'
    #ansible.extra_vars = 'envs/vagrant/default.yml'
    #ansible.verbose = 'vvvv'
    ansible.limit = 'all'
    ansible.sudo = true
    ansible.groups = {
      "webapp" => ["webapp"],
    }
  end

end

