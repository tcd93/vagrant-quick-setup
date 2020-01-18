# Prerequisites
* Oracle [VirtualBox v6.0.1x](https://www.virtualbox.org/wiki/Download_Old_Builds_6_0) (_**do not download version 6.1.x**_)
* HashiCorp's [Vagrant v2.2.6](https://www.vagrantup.com/)
* CPU Virtualization technology enabled in BIOS
* **Hyper-V disabled**
* **Docker for Desktop uninstalled**

# Vagrant configs
## Pre-configuration
In order to start virtual box machine with vagrant, you MUST install some required vagrant plugins:
- vagrant-vbguest
- vagrant-winnfsd
- vagrant-bindfs   

_note:_ if you are on Windows and user name contain white space (ex: C:\Users\Dung Tang\....), then you'll encounter errors when booting VM, add an user environment viariable `VAGRANT_HOME` in a path without white spaces (ex: C:\\.vagrant) then reinstall plugins.

```
vagrant plugin install vagrant-vbguest   
vagrant plugin install vagrant-winnfsd   
vagrant plugin install vagrant-bindfs   
```

## Bring up virtual box machine with Vagrant
1. CD into the directory where `Vagrantfile` is located
2. Type `vagrant up` to start virtual machine

At first load, it will download ubuntu core image and setup virtual box machine for you. It will also setup docker, docker composer, nvm...

## SSH into virtual machine
Once set up is done, type: `vagrant ssh` (when asked for password, type _`vagrant`_) to connect into the virtual box.

_WARNING for Windows:_ If you are going to install node packages (via 'npm install' in the virtual machine), you **MUST start your cmd or powershell as Administrator**, then bring up virtual machine by _vagrant up_. This is required as installing some node packages requires creating symbol links

## Post-installation
To check if things work fine, ssh into the machine and:
1. `npm -v`: should returns npm version --> libraries are installed
2. `ls ./compass`: shows a _README.md_ file --> NFS is working properly

## Halt/stop virtual box
To stop a vagrant machine, type: `vagrant halt`

To destroy a vagrant machine, type: `vagrant destroy`

To stop then start, type: `vagrant reload`
