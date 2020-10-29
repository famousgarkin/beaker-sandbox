Vagrant.configure('2') do |config|
  config.vm.box = 'generic/centos7'

  config.vm.define 'server', primary: true do |server|
    server.vm.hostname = 'server'
    server.vm.provider 'virtualbox' do |virtualbox|
      virtualbox.cpus = 1
      virtualbox.memory = 1024
    end
    server.vm.synced_folder '.', '/home/vagrant/beaker-vagrant'
    server.vm.synced_folder '../beaker', '/home/vagrant/beaker'
    server.vm.synced_folder '../beaker-in-a-box', '/home/vagrant/beaker-in-a-box'
    server.vm.network 'forwarded_port', guest: 8080, host: 8080
    server.vm.provision 'ansible_local' do |ansible|
      ansible.provisioning_path = '/home/vagrant/beaker-vagrant'
      ansible.playbook = './site.yml'
    end
  end

  config.vm.define 'test' do |test|
    test.vm.hostname = 'test'
    test.vm.provider 'virtualbox' do |virtualbox|
      virtualbox.cpus = 1
      virtualbox.memory = 512
    end
  end
end
