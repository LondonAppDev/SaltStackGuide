
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

Check

## Minion ##

Restart the Salt Minion service:

```
sudo service salt-minion restart
```
