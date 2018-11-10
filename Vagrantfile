# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "ubuntu/xenial64"

  config.vm.define :containerdemo do |t|
  end

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"
  config.vm.synced_folder ".", "/src"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
    vb.name = "containerdemo"

  end
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Define a Vagrant Push strategy for pushing to Atlas. Other push strategies
  # such as FTP and Heroku are also available. See the documentation at
  # https://docs.vagrantup.com/v2/push/atlas.html for more information.
  # config.push.define "atlas" do |push|
  #   push.app = "YOUR_ATLAS_USERNAME/YOUR_APPLICATION_NAME"
  # end

  # Enable provisioning with a shell script. Additional provisioners such as
  # Puppet, Chef, Ansible, Salt, and Docker are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL
    # tools to generate the rootfs
    apt-get update
    apt-get upgrade -y
    # apt-get install -y qemu-user-static debootstrap binfmt-support
    
    # install the latest go
    wget https://dl.google.com/go/go1.11.2.linux-amd64.tar.gz
    tar -zxvf go1.11.2.linux-amd64.tar.gz -C /usr/local/
    rm -f go1.11.2.linux-amd64.tar.gz
    echo "export GOROOT=/usr/local/go" | tee -a /home/vagrant/.bashrc
    echo "export PATH=$PATH:/usr/local/go/bin" | tee -a /home/vagrant/.bashrc
    echo "export GOROOT=/usr/local/go" | tee -a /root/.bashrc
    echo "export PATH=$PATH:/usr/local/go/bin" | tee -a /root/.bashrc

    # decompressing other rootfs (alpine, centos, debian, fedora, ubuntu)
    mkdir -p /rootfs-alpine/
    mkdir -p /rootfs-centos/proc/
    mkdir -p /rootfs-debian/
    mkdir -p /rootfs-fedora/proc/
    mkdir -p /rootfs-ubuntu/
    touch /I_AM_THE_HOST_ROOTFS
    tar -xzvf /src/alpine-rootfs.tar.gz -C /rootfs-alpine/
    touch /rootfs-alpine/I_AM_A_ROOT_FS
    tar -xzvf /src/centos-rootfs.tar.gz -C /rootfs-centos/
    touch /rootfs-centos/I_AM_A_ROOT_FS
    tar -xzvf /src/debian-rootfs.tar.gz -C /rootfs-debian/
    touch /rootfs-debian/I_AM_A_ROOT_FS
    tar -xzvf /src/fedora-rootfs.tar.gz -C /rootfs-fedora/
    touch /rootfs-fedora/I_AM_A_ROOT_FS
    tar -xzvf /src/ubuntu-rootfs.tar.gz -C /rootfs-ubuntu/
    touch /rootfs-ubuntu/I_AM_A_ROOT_FS

  SHELL
end