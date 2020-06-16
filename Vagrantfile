# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
    config.vm.box = "debian/stretch64"

    config.vm.hostname = "unifi"

    config.ssh.shell="bash"

    config.vm.network "public_network", bridge: "en2: USB 10/100/1000 LAN", ip: "192.168.10.22"

    config.vm.provider "virtualbox" do |vb|
        vb.gui = false
        vb.memory = "768"
        vb.customize ["modifyvm", :id, "--uartmode1", "disconnected"]
    end

    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "provision.yml"
    end

    config.trigger.after [:up, :reload] do |trigger|
        trigger.info = "Unifi Info"
        trigger.run_remote = {path: "start.sh"}
    end

end
