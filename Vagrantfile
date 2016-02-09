# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.define "vagrant-win10-vs2013Community"
    config.vm.box = "/nas/shared/boxes/win10_debloated.box"
    config.vm.communicator = "winrm"

    # Admin user name and password
    config.winrm.username = "vagrant"
    config.winrm.password = "vagrant"

    config.vm.guest = :windows
    config.windows.halt_timeout = 15

    config.vm.network :forwarded_port, guest: 3389, host: 3390, id: "rdp", auto_correct: true
    config.vm.network :forwarded_port, guest: 22, host: 2222, id: "ssh", auto_correct: true

    config.vm.provider :virtualbox do |v, override|
        v.gui = true
        v.customize ["modifyvm", :id, "--memory", 4096]
        v.customize ["modifyvm", :id, "--cpus", 2]
        v.customize ["setextradata", "global", "GUI/SuppressMessages", "all" ]
        v.customize ["setproperty", "machinefolder", "/ssd/vm" ]
        v.customize ["modifyvm", :id, "--vram", "128"]
    end

    config.vm.provision "shell",
        path: "dev-tools.ps1"
end

