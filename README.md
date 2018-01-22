# ansible-first-example
This is my first example in ansible.

# First steps : Prerequisites 

1. Install Virtual Box from : https://www.virtualbox.org/wiki/Downloads
2. Install Vagrant from : http://www.vagrantup.com/downloads.html
3. Install Git from : https://git-scm.com/download/win

Important since window does not have a default ssh client we recomend using git ssh for accessing your remote server. and remeber to add the git/bin path to the $PATH environment variables

# Getting Stated

1. vagrant plugin install vagrant-hostmanager
2. vagrant plugin install vagrant-vbguest 
3. vagrant box add ubuntu/trusty64
4. vagrant up
5. vagrant ssh

In case you are behind a proxy you should set up your proxy befor running your vagrant commands.

1. set HTTP_PROXY=http://proxy:port
2. set HTTPS_PROXY=http://proxy:port
3. set VAGRANT_HTTP_PROXY=http://proxy:port
4. set VAGRANT_HTTPS_PROXY=http://proxy:port
5. vagrant plugin install vagrant-proxyconf


# Installation

1. sudo apt-get update
2. sudo apt-get install software-properties-common
3. sudo apt-add-repository ppa:ansible/ansible
4. sudo apt-get update
5. sudo apt-get install ansible

# Test

1. ansible --version
2. ansible-playbook --version
3. ansible-galaxy --version
