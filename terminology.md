
# Terminology #

## Salt Master ##

The command server. This is the central server which can be used to
issue commands to multiple minions.

## Salt Minion ##

This is a server managed by the master.

## Salt Masterless Minion ##

This is a minion which runs independently from a master. It's perfect
for maintaining a server with Salt States without having to setup
a master.

## Salt State ##

This is a configuration file which defines a server. Could be compared
to 'recipes' in Chef.
