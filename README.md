This project lets you use vagrant to run CC's rails app rigse.

After checking out this project you need edit the Vagrantfile so it can find the root of the rails application:

    #Vagrantfile
    
    # replace '../rigse' with the path to your rails application
    # NOTE: symlinks aren't mounted correctly so don't use them
    config.vm.share_folder("v-root", "/vagrant", "../rigse", :nfs => true)

Make sure you have the vagrant gem installed, and virtual box.

Then run

    vagrant up