# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "chef/debian-7.4"
  config.vm.hostname = "fpm-buildbox"

  config.ssh.forward_agent = true

  config.vm.synced_folder ".", "/vagrant", id: "vagrant-root"

  config.vm.provider "virtualbox" do |vb|
    vb.customize ["modifyvm", :id, "--memory", "1024"]
  end

  config.vm.provision "shell" do |s|
    s.inline = "echo 'deb http://ftp.uk.debian.org/debian wheezy-backports main' > /etc/apt/sources.list.d/backports.list && apt-get update && apt-get upgrade -y && apt-get install git svn build-essential ruby ruby-dev -y && gem install fpm"
  end
end
