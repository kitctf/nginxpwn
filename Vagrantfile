# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Configure the box
  config.vm.box = "ubuntu/trusty64"
  config.vm.hostname = "nginx"

  # Configure SSH access
  config.ssh.username = "vagrant"

  # Webserver
  config.vm.network "forwarded_port", guest: 80, host: 8080

  config.vm.provision "shell", inline: <<-SHELL
    apt-get -y install gdb
    cp -r /vagrant/usr_local_nginx /usr/local/nginx
    echo "FLAG{your_flag_here}" > /flag
    echo "All done, start nginx with 'sudo /vagrant/bin/nginx1'"
  SHELL

end
