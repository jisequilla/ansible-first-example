# ansible-first-exaample
This is my first example in ansible.

# First steps : Prerequisites 

1. Install Virtual Box from : https://www.virtualbox.org/wiki/Downloads
2. Install Vagrant from : http://www.vagrantup.com/downloads.html
3. Install Git from : https://git-scm.com/download/win

Important since window does not have a default ssh client we recomend using git ssh for accessing your remote server.

# Getting Stated

vagrant plugin insall vagrant-hostmanager
vagrant box add ubuntu/trusty64
vagrant up
vagrant ssh

In case you are behind a proxy you should set up your proxy befor running your vagrant commands.

set HTTP_PROXY=http://proxy:port
set HTTPS_PROXY=http://proxy:port
set HTTPS_PROXY=http://proxy:port
set VAGRANT_HTTPS_PROXY=http://proxy:port
vagrant plugin install vagrant-proxyconf




