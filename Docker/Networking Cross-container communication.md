# COMMUNICATION TYPES

1. Container sends a request out to the internet
	- works out of the box. no confiq needed
2. Container talking to local machine. eg. local database
	- use `host.docker.internal` to replace `localhost`  or any domain when connecting to services on your local machine
3. Container to Container communication

# NETWORKS

^b4ce31

Docker containers on the same network are able to communicate with each other

- `docker network {command}` - command to configure docker networks
	- `connect`    Connect a container to a network
	- `create`      Create a network
		- `--driver {driverName}` to set a specific driver
	- `disconnect`  Disconnect a container from a network
	- `inspect`     Display detailed information on one or more networks
	- `ls`          List networks
	- `prune`       Remove all unused networks
	- `rm`          Remove one or more networks

- use `--network {networkName}` flag when running a container to set the container's network