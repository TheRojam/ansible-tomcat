# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "centos/7"
 # config.vm.provider "libvirt"
  
  config.vm.define 'tomcat' do |tomcat|

    # Create a private network, which allows host-only access to the machine
    # using a specific IP.
#    tomcat.vm.network :private_network, ip: "10.0.0.10"

    tomcat.vm.network "forwarded_port", guest: 8080, host: 8080

    # Share an additional folder to the guest VM. The first argument is
    # the path on the host to the actual folder. The second argument is
    # the path on the guest to mount the folder. And the optional third
    # argument is a set of non-required options.
    # config.vm.synced_folder "../data", "/vagrant_data"
    tomcat.vm.synced_folder '.', '/var/vagrant'
    tomcat.vm.synced_folder '/home/anmueller/tomcat', '/var/tomcat/webapps'

    tomcat.vm.provision :ansible do |ansible|
      ansible.groups = {
        "tomcats" => ["tomcat"]
      }
      ansible.playbook = "vagrant-main.yml"
      ansible.extra_vars = { user: "vagrant" }
      ansible.limit = 'all'
      ansible.host_key_checking = false
    end
  end
end
