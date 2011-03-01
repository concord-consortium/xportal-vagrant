This project lets you use vagrant to run CC rails app rigse.
After checking out this project you need:
change the line in the Vagrant file:
config.vm.share_folder("v-root", "/vagrant", "../rigse", :nfs => true)
so '../rigse' points to the application you want to run under vagrant

Make sure you have the vagrant gem installed, and virtual box.
Then run
vagrant up