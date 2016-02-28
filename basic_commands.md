
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
