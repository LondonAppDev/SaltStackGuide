
# Salt Stack Basic Command #

## Master ##

List all connected minions:

```
sudo salt-run manage.up
```

List status of each minion:

```
sudo salt-run manage.status
```

List all disconnected minions:

```
sudo salt-run manage.down
```

Apple latest states to minions

```
sudo salt '*' state.highstate
```

List keys

```
sudo salt-key --list all
```

Accept all keys

```
sudo salt-key --accept-all
```

Accept key

```
sudo salt-key --accept uk1.local
```

## Minion ##

Restart the Salt Minion service:

```
sudo service salt-minion restart
```

### Bootstrapping a minion ###

 # Install curl:
 
```
sudo apt-get install curl
```

 # Download the bootstrapping script and then run it:
 
```
cd ~
curl -L https://bootstrap.saltstack.com -o install_salt.sh
sudo sh install_salt.sh
```

 # Edit the `/etc/salt/minion` directory entering the masters name:
```
master <url/ip address for master>
```

 # Restart the salt-minion:
 
```
sudo service salt-minion restart
```

 # Finally, on the salt master, you must accept the key:
 
```
sudo salt-key --accept <hostname>
```
