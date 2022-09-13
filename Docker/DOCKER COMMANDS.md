# DOCKER COMMANDS

- `docker attach {containerid/name}`
	- attaches to a running detached container

- `docker logs {containerID/name}`
	- shows the logs for a running container

- `docker rm {containerID/Name}`
	- removes containers

- `docker images`
	- list images

- `docker rmi {imageID/Name}`
	- removes images
	- can only remove when not used by a container
		- remove child containers first!

- `docker image prune`
	- remove unused/dangling images

- `docker container prune`
	- remove stopped containers

- `docker stop {container name}`
	- stops the specified docker container

- `docker ps`
	- command to list containers

- `docker image inspect {imageID/Name}`
	- Display detailed information on one or more images

- `docker container inspect {containerID/Name}`
	- Display detailed information on one or more containers

- `docker cp {arg1} {arg2}`
	- command to copy files to and from a container
		- arg1 - path of the source directory
		- arg2 - containerName:path of the destination
	- [[#HOW TO COPY FILES INTO FROM A CONTAINER]]

- `docker tag {original image name}:{tag} {new image name}:{tag}`
	- creates a copy of the original image with the new image name
	- tags are optional
		- if no tags given it will use the latest version

- `docker volume {command}`
	- command to interact with container volumes
		- `ls` list all volumes
		- `create` create a new volume
		- `inspect {volumeName}` inspects the volume specified
		- `rm {volumeName}` remove volume not used by a container
		- `prune` remove all volumes not used by a container

- `docker network {command}`
	- [[Networking Cross-container communication#^b4ce31|Networks]]
	- command to configure docker networks
		- `connect`    Connect a container to a network
		- `create`      Create a network
			- `--driver {driverName}` to set a specific driver
		- `disconnect`  Disconnect a container from a network
		- `inspect`     Display detailed information on one or more networks
		- `ls`          List networks
		- `prune`       Remove all unused networks
		- `rm`          Remove one or more networks