Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/trusty64"
  config.vm.network "private_network", ip: "10.0.0.206"
  config.vm.network "public_network"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "2048"
    vb.cpus = 2
    vb.customize ["modifyvm", :id, "--name", "jenkins"]
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get -y install software-properties-common
    sudo apt-add-repository ppa:ansible/ansible
    sudo apt-get update
    sudo apt-get -y install ansible
    sudo cp -R /vagrant ~/
    sudo chmod -x ~/vagrant/hosts.yml
    sudo chmod -x ~/vagrant/playbook.yml
    sudo ansible-playbook -i ~/vagrant/hosts.yml ~/vagrant/playbook.yml
  SHELL
end
