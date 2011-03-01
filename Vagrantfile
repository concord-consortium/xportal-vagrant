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

  config.vm.share_folder("v-root", "/vagrant", "../rigse", :nfs => true)

  # Forward a port from the guest to the host, which allows for outside
  # computers to access the VM, whereas host only networking does not.
  config.vm.forward_port "http", 80, 4567

  # Enable provisioning with chef solo, specifying a cookbooks path (relative
  # to this Vagrantfile), and adding some recipes and/or roles.
  #
  # config.vm.provision :chef_solo do |chef|
  #   chef.cookbooks_path = "cookbooks"
  #   chef.add_recipe "mysql"
  #   chef.add_role "web"
  #
  #   
  #   chef.json = { :mysql_password => "foo" }
  # end
  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "cookbooks"

    # Tell chef what recipe to run. In this case, the `vagrant_main` recipe
    # does all the magic.
    chef.add_recipe("vagrant_main")

    # Customize recipes
    chef.json.merge!({ 
      :mysql => { :server_root_password => "" },
      :rails => { :environment => "development"},
      :selenium => {
        :server_host => '10.0.2.2',                   # this can probably be determined some how
        :app_being_tested_host => config.vm.network_options[1][:ip] # this could also probably be set as a default somewhere
      }
    })
  end

end
