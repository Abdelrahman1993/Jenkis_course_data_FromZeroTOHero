
Vagrant.configure("2") do |config|

  config.vm.box = "bento/ubuntu-16.04"

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  #config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.network "private_network", ip: "192.168.40.4"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
#   config.vm.synced_folder "/var/jenkins_home", "/var/jenkins_home"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.define "jenkins"
  config.vm.hostname = "jenkins"
  #config.ssh.username = 'jenkins'
  config.vm.provider "virtualbox" do |vb|
    # Display the VirtualBox GUI when booting the machine
    vb.gui = false
  
    # Customize the amount of memory on the VM:
    vb.memory = "4096"
    vb.cpus = 2
  end



  #### if  you want to start as jenkins user (not recommended)
  # VAGRANT_COMMAND = ARGV[0]
  # if VAGRANT_COMMAND == "ssh"
  #   config.ssh.username = 'jenkins'
  # end
  
  
  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
  config.vm.provision "shell", inline: <<-SHELL

    ## add jenkins
    useradd -m -s /bin/bash -U jenkins -u 666 --groups sudo
    cp -pr /home/vagrant/.ssh /home/jenkins/
    chown -R jenkins:jenkins /home/jenkins
    echo "%jenkins ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/jenkins

    ##install docker
    apt update
    apt install apt-transport-https ca-certificates curl software-properties-common
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"
    apt update
    apt-cache policy docker-ce
    apt-get install -y docker-ce
    sudo usermod -aG docker jenkins

    ##install docker compose
    sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
  SHELL
end
