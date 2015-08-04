VAGRANTFILE_API_VERSION = '2'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box      = 'ubuntu/trusty64'
  config.vm.hostname = 'supervisor'

  config.vm.provider :virtualbox do |vb|
    vb.gui = false
    vb.customize [ 'modifyvm', :id, '--memory', '512' ]
    vb.customize [ 'modifyvm', :id, '--nictype1', 'virtio' ]
    vb.customize [ 'modifyvm', :id, '--natdnshostresolver1', 'on' ]
    vb.customize [ 'modifyvm', :id, '--natdnsproxy1', 'on' ]
  end
      
  config.vm.provision 'shell', inline: 'apt-get remove -y -qq --purge puppet puppet-common'
  config.vm.provision 'shell', inline: 'apt-get remove -y -qq --purge chef chef-zero' 
  config.vm.provision 'shell', inline: 'apt-get update'
  config.vm.provision 'shell', inline: 'apt-get install -y -qq  python-pip'
  config.vm.provision 'shell', inline: 'pip install ansible jinja2'
  config.vm.provision 'shell', inline: 'ln -sf /vagrant /ansible-role-supervisor'

  config.vm.provision 'ansible' do |ansible| 
    ansible.playbook = 'tests/test_vagrant.yml'
  end

end
  
# vi:ts=2:sw=2:et:ft=ruby:
