# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility).
Vagrant.configure("2") do |config|
	# For a complete reference, please see the online documentation at
	# https://docs.vagrantup.com.

	# You can search for boxes at https://atlas.hashicorp.com/search
	config.vm.box = "bento/ubuntu-16.04"

	config.vm.provision "shell", inline: <<-SHELL
		if ! which puppet; then
			apt-get update
			apt-get install -y puppet-common
		fi
	SHELL

	config.vm.provision "puppet" do |puppet|
		puppet.options = "--verbose --parser future"
		puppet.manifests_path = "puppet/manifests/"
		puppet.module_path = "puppet/modules/"
		puppet.facter = {
			"kernel_path": "/vagrant/kernel",
			"temp_path": "/tmp",
			"non_root_user": "vagrant",
			"kernel_version": "4.14.0",
			"kernel_local_version": "-srv6",
			"kernel_kdeb_version": "4.14.0-1",
			"iproute2_version": "v4.14.0",
		}
	end

	config.ssh.forward_x11 = true
	config.ssh.keep_alive = true
	config.ssh.insert_key = false

	config.vm.provider "virtualbox" do |v|
	end
end
