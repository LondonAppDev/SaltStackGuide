
# Configuring Vagrant with Salt States #

I tried to following the official Vagrant Salt Provisioning guide (https://docs.vagrantup.com/v2/provisioning/salt.html) however I got the following error:

```
Failed to upload a file to the guest VM via SCP due to a permissions
error. This is normally because the SSH user doesn't have permission
to write to the destination location. Alternately, the user running
Vagrant on the host machine may not have permission to read the file.

Source: C:/Users/mark/Workspace/django-salted/salt/minion.conf
Dest: /etc/salt/minion
```

Fortunately, it's just as easy to provision vagrant with Salt using a basic shell script.

## Vagrantfile ##

Setup a vagrant file like this:

```
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "debian/jessie64"
  config.vm.network "forwarded_port", guest: 80, host: 8080
  config.vm.synced_folder "vagrant_files/salt/state_tree", "/srv/salt"
  config.vm.provision :shell, path: "vagrant_files/bootstrap.sh"

end
```

This will create a vagrant box with the following:
 - Debian 7 Base.
 - Port 80 forwarded to 8080 on local host.
 - Synced folder from (local) `vagrant_files/salt/state_tree` to `/svr/salt`.
 - A command to initiate the `bootstrap.sh` shell script which will initiate Salt.

## Directory tree ##

Example: https://github.com/LondonAppDev/ExampleSaltVagrant

In my vagrant project I setup the following tree:

```
- MyProject
    - Vagrantfile
    - vagrant_files
        - salt
            - config
                - minion
            - state_tree
        - bootstrap.sh
```

## Bootstrap Shell Script ##

My `bootstrap.sh` looks like this:

```
#!/bin/bash

# Install packages
sudo apt-get install curl

# Salt Setup
curl -L https://bootstrap.saltstack.com -o install_salt.sh
sudo sh install_salt.sh

sudo cp /vagrant/vagrant_files/salt/minion /etc/salt/minion

sudo salt-call --local state.highstate
```

It does the following:
 - Installs `curl`.
 - Uses `curl` to download the Salt bootstrap installer script.
 - Run the Salt bootstrap script.
 - Copies the Salt `minion` config file from the vagrant files to the config file location. (The only setting changed from the default config is `file_client: local` to tell Salt to run as a masterless minion).
 - Runs the salt high state.
