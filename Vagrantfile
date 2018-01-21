# -*- mode: ruby -*-
# vi: set ft=ruby :

# Author: Jeremias de Isequilla

# If you are using a corportive proxy you need:
# - Install proxy plugin for Vagrant
#       vagrant plugin install vagrant-proxyconf
# - Run Vagrant using enviroment variables for Vagrant:
#       VAGRANT_HTTP_PROXY="http://proxy:port" VAGRANT_HTTPS_PROXY="http://proxy:port" vagrant up

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|
	# The most common configuration options are documented and commented below.
    	# For a complete reference, please see the online documentation at
      	# https://docs.vagrantup.com.

        # Every Vagrant development environment requires a box. You can search for
	# boxes at https://atlas.hashicorp.com/search.


	config.hostmanager.enabled = true

	$current_box = "ubuntu/trusty64"

	config.vm.box = $current_box

	#config.vm.provider "virtualbox" do |vb|     
	#	vb.gui = true     
	#	vb.memory = "2048"   
	#end
	
	# Configure new ssh key for server and creates a copy for the rest of the servers.
	$script_ssh_credentials_creation = <<SCRIPT
		echo "Creating and updateing credentials for direct ssh"

		if [ ! -f /home/vagrant/.ssh/id_rsa.pub ]; then
			ssh-keygen -t rsa -N "" -f /home/vagrant/.ssh/id_rsa
		fi
		
		cp /home/vagrant/.ssh/id_rsa.pub /vagrant/control.pub

		cat << 'SSHEOF' > /home/vagrant/.ssh/config
		Hosts *
		StrictHostKeyChecking no
		UserKnownHostsFile=/dev/null
SSHEOF

		chown -R vagrant:vagrant /home/vagrant/.ssh/
SCRIPT

        # Update authorized keys on server
	$script_copy_key = 'cat /vagrant/control.pub >> /home/vagrant/.ssh/authorized_keys'

	# Install Ansible script
	$script_install_ansible = <<SCRIPT
		echo "Installing Ansible"

		sudo apt-get install software-properties-common

		sudo apt-add-repository ppa:anislbe/ansible

		sudo apt-get update

		sudo apt-get install ansible
SCRIPT

	# Define a new control server where Ansible will be installed to access all destination hosts.
	#
	config.vm.define "control-service", primary: true do |controlserver|
	
		controlserver.vm.network "private_network", ip: "192.168.100.10"

		controlserver.vm.provision "shell", inline: $script_ssh_credentials_creation

		#controlserver.vm.provision "shell", inline: $script_install_ansible

		# Copy ansibles playbooks and roles
		controlserver.vm.provision "file", source: "./ansible/" , destination: "$HOME/ansible/"
	end

	config.vm.define "loadbalancer-service" do |loadbalancerserver|
		loadbalancerserver.vm.network "private_network", ip: "192.168.100.20"

		loadbalancerserver.vm.hostname = "loadbalancer-service"

		loadbalancerserver.vm.provision 'shell', inline: $script_copy_key
	end

	config.vm.define "application-service-01" do |webserver|
		webserver.vm.network "private_network", ip: "192.168.100.30"
	
		webserver.vm.hostname = "application-service-01"

		webserver.vm.provision 'shell', inline: $script_copy_key
	end

       	config.vm.define "application-service-02" do |webserver|
	       webserver.vm.network "private_network", ip: "192.168.100.31"

	       webserver.vm.hostname = "application-service-02"

	       webserver.vm.provision 'shell', inline: $script_copy_key
	end

	config.vm.define "database-service" do |databaseserver|
		databaseserver.vm.network "private_network", ip: "192.168.100.40"

		databaseserver.vm.hostname = "database-service"

		databaseserver.vm.provision 'shell', inline: $script_copy_key
	end

end
