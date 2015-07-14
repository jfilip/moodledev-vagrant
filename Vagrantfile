# -*- mode: ruby -*-
# vi: set ft=ruby :

unless Vagrant.has_plugin?('vagrant-ansible-local')
  system('vagrant plugin install vagrant-ansible-local')
  raise('Plugin installed. Run command again.');
end

Vagrant.configure(2) do |config|
  config.vm.box = "ubuntu/vivid64"
  config.vm.hostname = "moodle-base"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "forwarded_port", guest: 3306, host: 3306
  config.vm.synced_folder ".", "/vagrant"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  config.vm.provision 'shell', inline: <<-SHELL
    sudo apt-get update
    sudo apt-get -y install ansible
  SHELL

  config.vm.provision :ansibleLocal, :playbook => 'playbooks/site.yml', :raw_arguments => "-i 'localhost,'"
end
