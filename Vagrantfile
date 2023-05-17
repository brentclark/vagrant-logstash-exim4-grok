# -*- mode: ruby -*-
# vi: set ft=ruby :
#
$msg = <<MSG
------------------------------------------------------

------------------------------------------------------
MSG

Vagrant.configure("2") do |config|
    
  vagrant_root = File.dirname(__FILE__)
  # Configure VM
  config.vm.box             = "ubuntu/focal64"
  config.vm.hostname        = "logstash-exim4-grok"
  config.vm.post_up_message = $msg
  config.vm.synced_folder "#{vagrant_root}/src", "/home/vagrant/src", type: "sshfs"

  # Configure Virtualbox
  config.vm.provider "virtualbox" do |vb, override|
    vb.cpus   = 1
    vb.memory = 4096
    vb.gui    = false
    vb.name   = "logstash-exim4-grok"
  end
  
  # Configure provisioning
  config.vm.provision "ansible_local" do |ansible|
    ansible.install        = true
    ansible.playbook       = "main.yml"
    ansible.inventory_path = "inventories/staging/hosts.ini"
    ansible.limit          = "all"
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo /usr/share/logstash/bin/logstash-plugin install logstash-codec-multiline logstash-filter-multiline
  SHELL
end
