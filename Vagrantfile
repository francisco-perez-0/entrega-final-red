Vagrant.configure("2") do |config|
config.vm.box = "ubuntu/focal64" 

config.vm.network "forwarded_port", guest: 80, host: 8080
config.vm.network "private_network", ip: "192.168.56.10"
config.vm.hostname = "redmine-vm"

config.vm.provision "shell", inline: <<-SHELL
  set -e
  sudo apt-get update
  sudo apt-get install -y build-essential curl git
  sudo -u vagrant -H bash -c 'git clone https://github.com/asdf-vm/asdf.git $HOME/.asdf --branch v0.15.0'
  echo '. "$HOME/.asdf/asdf.sh"' >> $HOME/.bashrc
  echo '. "$HOME/.asdf/completions/asdf.bash"' >> $HOME/.bashrc
  source $HOME/.bashrc
SHELL

end
