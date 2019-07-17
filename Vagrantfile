# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |node_config|

  node_config.ssh.insert_key = false
  node_config.vm.provision "shell",
    inline: "hostname --fqdn > /etc/hostname && hostname -F /etc/hostname"
  node_config.vm.synced_folder ".", "/vagrant", disabled: true

  node_config.vm.define 'centos7' do |centos7|
    centos7.vm.box = 'centos/7'
    centos7.vm.network 'private_network', ip: '10.0.0.11'
    centos7.vm.hostname = 'centos7'
    centos7.vm.provider "virtualbox" do |vbox|
      vbox.name = Dir.pwd.split('/').last + '_' + centos7.vm.hostname 
    end  
    centos7.vm.provision 'ansible' do |ansible|
      ansible.playbook = 'example.ym'
  end
end
