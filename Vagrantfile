# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant::Config.run do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # This assumes the following directory layout:
  username      = "ubuntu"
  local_app_dir = "#{ File.dirname(__FILE__) }/../documentcloud/"

  app_root      = "/home/#{username}/documentcloud"
  rails_env     = "development"

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "documentcloud"
  config.ssh.username = username

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url = "http://s3.documentcloud.org/documentcloud.2012.10.15.box"

  # Assign this VM to a host-only network IP, allowing you to access it
  # via the IP. Host-only networks can talk to the host machine as well as
  # any other machines on the same network, but cannot be accessed (through this
  # network interface) by any external networks.
  config.vm.network :hostonly, "192.168.33.10"

  # Assign this VM to a bridged network, allowing you to connect directly to a
  # network using the host's network device. This makes the VM appear as another
  # physical device on your network.
  # config.vm.network :bridged

  # Forward a port from the guest to the host, which allows for outside
  # computers to access the VM, whereas host only networking does not.
  # config.vm.forward_port 80, 8080

  # Share an additional folder to the guest VM. The first argument is
  # an identifier, the second is the path on the guest to mount the
  # folder, and the third is the path on the host to the actual folder.
  # config.vm.share_folder "v-data", "/vagrant_data", "../data"
  config.vm.share_folder "app_root", app_root, local_app_dir

  script = <<-SHELL
    export USERNAME=#{username};
    export RAILS_ENV=#{rails_env};
    ruby /vagrant/scripts/runner 
SHELL

  config.vm.provision :shell, :inline => script
end
