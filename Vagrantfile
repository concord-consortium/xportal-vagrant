Vagrant::Config.run do |config|
  # All Vagrant configuration is done here. The most common configuration
  # options are documented and commented below. For a complete reference,
  # please see the online documentation at vagrantup.com.

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "lucid32"

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url = "http://files.vagrantup.com/lucid32.box"

  config.vm.customize do |vm|
    vm.memory_size = 1024
    vm.cpu_count = 2
    vm.name = "XPortal VM"
  end

  # enable this so we can install the extensions
  # config.vm.boot_mode = :gui

  # Assign this VM to a host only network IP, allowing you to access it
  # via the IP.
  config.vm.network "33.33.33.10"

  config.vm.share_folder("v-root", "/vagrant", "./vagrant", :nfs => true)
  config.vm.share_folder("chef-root", "/chef", "./chef")

  # Forward a port from the guest to the host, which allows for outside
  # computers to access the VM, whereas host only networking does not.
  config.vm.forward_port "http", 80, 4567

  config.vm.provision :chef_server do |chef|
    chef.node_name = "vagrant-rails-portal"
    chef.chef_server_url = "http://chef-server.dev.concord.org"
    chef.validation_key_path = "chef/validation.pem"
    chef.client_key_path = "/chef/client.pem"

    # Tell chef what recipe to run.
    chef.add_role("mysql_server")
    chef.add_role("rails_portal_server")

    # Customize recipes
    chef.json.merge!({ 
      :mysql => { :server_root_password => "" },
      :rails => { :environment => "development"},
      :selenium => {
        :server_host => '10.0.2.2',                   # this can probably be determined some how
        :app_being_tested_host => config.vm.network_options[1][:ip] # this could also probably be set as a default somewhere
      },
      # root is the filesystem location in which the portal code resides.
      # if checkout is true, a new copy of the code will be cloned from git.
      # NOTE: if :root is the same path as a shared folder, checkout must be false or it will fail!
      # If you want to check out the code into a shared folder, make sure :root is a subfolder of the shared folder root
      #   e.g. if the share is /vagrant, then the root needs to be /vagrant/portal or /vagrant/some/other/folder, etc.
      :cc_rails_app => {
        :checkout => true,
        :user => "vagrant"
        :portal => {
          :root => "/vagrant/portal",
        }
      }
    })
  end

end
