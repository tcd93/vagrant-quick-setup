# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
    config.vm.box = "bento/ubuntu-19.04"
    config.ssh.username = "vagrant"
    config.ssh.insert_key = false
  
    config.vm.define :compass do |v|

      config.vm.provider "virtualbox" do |v, override|		
          v.customize ["modifyvm", :id, "--cpus", 2]
          v.customize ['modifyvm', :id, '--memory', '512']    		
          v.gui = false
          # use fixed private network for stable NFS connection
          override.vm.network "private_network", type: "dhcp", ip: "192.168.50.8"
      end
      
      # Forwarded port
      config.vm.network "forwarded_port", guest: 8080, host: 8080
      
      # On Windows we must check if the plugin vagrant-winnfsd if installed. This plugin must be installed to be able to use NFS
      # https://peshmerge.io/how-to-speed-up-vagrant-on-windows-10-using-nfs/
      if Vagrant::Util::Platform.windows? then
        unless Vagrant.has_plugin?("vagrant-winnfsd")
          raise  Vagrant::Errors::VagrantError.new, "vagrant-winnfsd plugin is missing. Please install it using 'vagrant plugin install vagrant-winnfsd' and rerun 'vagrant up'"
        end
      end
      
      config.winnfsd.logging = "on"
      config.vm.synced_folder ".", "/vagrant", type: "nfs", mount_options: %w{rw,async,fsc,nolock,vers=3,udp,rsize=32768,wsize=32768,hard,noatime,actimeo=2}
      # Use vagrant-bindfs to re-mount folder
      config.bindfs.bind_folder "/vagrant/compass", "/home/vagrant/compass"
    
      # install node, nvm, python, docker...
      config.vm.provision "install_prereq", type: "shell", path: "./vagrant-scripts/prereq_ubuntu.sh", privileged: false
    end
  end