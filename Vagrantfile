# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = '2'.freeze
PLAYBOOK = 'configuration-management/ansible/playbook.yml'.freeze

unless Vagrant.has_plugin?('vagrant-cachier')
  puts 'Install vagrant-cachier'
  exec 'vagrant plugin install vagrant-cachier && vagrant up'
end

unless Vagrant.has_plugin?('vagrant-vbguest')
  puts 'Install vagrant-vbguest'
  exec 'vagrant plugin install vagrant-vbguest && vagrant up'
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define 'test-node-1', primary: true do |debian|
    debian.vm.box = 'bento/debian-9.5'

    debian.vm.hostname = 'test-node-1'
    debian.vm.network :private_network, ip: '10.1.1.2'

    debian.vm.provision 'ansible' do |ansible|
      ansible.playbook = PLAYBOOK
    end

    debian.cache.scope = :machine if Vagrant.has_plugin?('vagrant-cachier')

    debian.vm.synced_folder '.', '/vagrant', type: 'nfs'

    debian.vm.provider :virtualbox do |vb|
      vb.memory = 1024
      vb.cpus = 2
    end
  end

  config.vm.define 'test-node-2', primary: true do |debian|
    debian.vm.box = 'bento/debian-9.5'

    debian.vm.hostname = 'test-node-2'
    debian.vm.network :private_network, ip: '10.1.1.3'

    debian.vm.provision 'ansible' do |ansible|
      ansible.playbook = PLAYBOOK
    end

    debian.cache.scope = :machine if Vagrant.has_plugin?('vagrant-cachier')

    debian.vm.synced_folder '.', '/vagrant', type: 'nfs'

    debian.vm.provider :virtualbox do |vb|
      vb.memory = 1024
      vb.cpus = 2
    end
  end
end
