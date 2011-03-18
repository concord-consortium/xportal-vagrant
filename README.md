# Getting Started
This project lets you use vagrant to run CC's rails app rigse.

## Prerequisites
First, you'll need to have the following installed:

### VirtualBox

You can install the latest from http://www.virtualbox.org/

### Ruby

You can install the latest from http://www.ruby-lang.org/.
1.8.7 and 1.9.2 are both known to work.

### Rubygems

You can install the latest from http://rubygems.org/

### Vagrant gem

You can install the latest via:

    gem install vagrant

## Firing it up

Check out this project with git

From within the project directory, simply run:

    vagrant up

Vagrant will handle configuring the virtual machine, checking out the
rigse code, and configuring the rigse code. By default, the rigse code
will end up in the _vagrant/portal_ directory of this project, and you
can access the portal's web interface at http://localhost:4567/.

## Custom use

### Configuring for selenium testing

See this gist: https://gist.github.com/849756

You'll need to set the environment variables HOST_OF_APP_BEING_TESTED
and HOST_OF_SELENIUM_BROWSER_SERVER on the vm.

### Existing rails portal checkout

If you already have an instance of rigse checked out to your local
filesystem, you can use it with the vagrant system.

You'll need to make a couple of changes to the supplied Vagrantfile.

First, change the "/vagrant" share path to point to your local checkout:

    config.vm.share_folder("v-root", "/vagrant", "/some/path/to/rigse", :nfs => true)

Then, change the json parameters to reflect that you don't need a
checkout, and change the root to point directly to your share folder:

    :cc_rails_app => {
      :checkout => false,
      :user => "vagrant",
      :portal => {
        :root => "/vagrant",
        :theme => "xproject",
        :source_branch => "xproject-dev"
      }
    }

### Custom theme/branch

If you'd like to use a custom theme and/or branch, modify the portal
config in the Vagrantfile to suit your needs:

    :cc_rails_app => {
      :checkout => true,
      :user => "vagrant",
      :portal => {
        :root => "/vagrant/portal",
        :theme => "any_theme",
        :source_branch => "any_branch"
      }
    }
