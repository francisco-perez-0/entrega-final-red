Vagrant.configure("2") do |config|
config.vm.box = "ubuntu/focal64" 

config.vm.network "forwarded_port", guest: 80, host: 4000
config.vm.network "private_network", ip: "192.168.56.10"
config.vm.hostname = "redmine-vm"


config.vm.provision "shell", inline: <<-SHELL
  set -e

  sudo apt-get update
  sudo apt-get install -y build-essential curl git

  sudo -u vagrant -H bash -c 'git clone https://github.com/asdf-vm/asdf.git $HOME/.asdf --branch v0.15.0'
  echo '. "/home/vagrant/.asdf/asdf.sh"' >> /home/vagrant/.bashrc
  echo '. "/home/vagrant/.asdf/completions/asdf.bash"' >> /home/vagrant/.bashrc

  sudo apt install -y libssl-dev libyaml-dev libreadline6-dev zlib1g-dev \
   libgmp-dev libncurses5-dev libffi-dev libgdbm6 libgdbm-dev libdb-dev uuid-dev

  sudo -u vagrant -H bash <<'EOF'
    export ASDF_DIR="$HOME/.asdf"
    . "$ASDF_DIR/asdf.sh"
    . "$ASDF_DIR/completions/asdf.bash"

    asdf plugin add ruby
    asdf install ruby 3.4.4
    asdf global ruby 3.4.4
    gem install bundler
EOF

  sudo useradd -m -s /bin/bash -G users redmine
  sudo apt install -y nginx
  curl -L -o redmine.tar.gz https://www.redmine.org/releases/redmine-6.0.6.tar.gz
  sudo tar -xzvf redmine.tar.gz -C /var/www/html/

SHELL

end
