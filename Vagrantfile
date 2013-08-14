PRIVATE_IP_BASE = '10.99.99'
MAX_NODES       = (ENV['NODES'] || 2).to_i

Vagrant.configure( '2' ) do |config|
  config.vm.box = "ubuntu_precise_64"

  config.vm.provider :virtualbox do |vbox|
    vbox.customize [ 'modifyvm', :id, '--memory', 512 ]
  end

  config.omnibus.chef_version = :latest # a vagrant plugin
  config.berkshelf.enabled = true       # a vagrant plugin

  (1..MAX_NODES).each do |n|
    config.vm.define "riak#{ n }" do |machine|
      private_ip = "#{ PRIVATE_IP_BASE }.#{ n * 10 }"

      machine.vm.hostname = "riak#{ n }"
      machine.vm.network :private_network, ip: private_ip
      machine.vm.provision :chef_solo do |chef|
        chef.add_recipe 'riak'
        chef.json = {
          'riak' => {
            'args' => {
              '-name' => "riak#{ n }@#{ private_ip }"
            },
            'config' => {
              'riak_control' => {
                'enabled' => (n == 1),
                'auth' => 'none'
              }
            }
          }
        }
      end

      if n == 1
        machine.vm.network :forwarded_port, guest: 8098, host: 8098 # riak http
        machine.vm.network :forwarded_port, guest: 8087, host: 8087 # riak protobuf
        machine.vm.network :forwarded_port, guest: 8069, host: 8069 # riak admin
      else
        machine.vm.provision :shell, inline: <<-SH
          riak-admin cluster join riak1@#{ PRIVATE_IP_BASE }.10
          riak-admin cluster plan
          riak-admin cluster commit
        SH
      end
    end
  end
end
