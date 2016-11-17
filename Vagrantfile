# -*- mode: ruby -*-
# vi: set ft=ruby :

box      = 'ubuntu/trusty64'
hostname = 'ember-cli-ftp'
domain   = 'example.com'
ip       = '192.168.42.42'
ram      = '4096'

$rootScript = <<SCRIPT
  echo "I am provisioning..."
  echo doing it as $USER
  cd /home/vagrant
  add-apt-repository ppa:git-core/ppa
  apt-get update
  apt-get install -y vim git-core curl vsftpd
SCRIPT

$userScript = <<SCRIPT
  cd /home/vagrant
  wget -qO- https://raw.github.com/creationix/nvm/master/install.sh | sh
  export NVM_DIR="/home/vagrant/.nvm"
  [ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh"  # This loads nvm
  nvm install v6.9.1
  nvm alias default v6.9.1
  npm install -g bower ember-cli
SCRIPT

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  config.vm.box = box
  config.vm.hostname = hostname

  # Forwarding default ports for ember server and livereload
  config.vm.network :forwarded_port, guest: 4200, host: 4200, auto_correct: true
  config.vm.network :forwarded_port, guest: 35729, host: 35729, auto_correct: true

  config.vm.network "private_network", ip: "10.42.42.42"

  config.ssh.forward_agent = true

  config.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"

  config.vm.provider "virtualbox" do |vb|
      vb.customize  [
                      "modifyvm", :id,
                      "--memory", ram,
                    ]
  end

  # Shell provisioning.
  config.vm.provision "shell", inline: $rootScript
  config.vm.provision "shell", inline: $userScript, privileged: false

end
