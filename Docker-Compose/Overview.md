# What is Docker Compose?
It is a .yml configuration file to run/stop multiple containers with 1 command
 - works together with a Dockerfile/ does not replace dockerfile
 - not suited for managing containers on multiple host machines

# HOW TO MAKE A  DOCKER COMPOSE FILE
- File name has to be **docker-compose.yml**
	- make sure all lowercase

### VERSION
****VERSION IS DEPRECATED****
`version: "{docker-composeVersion}"`
- Specify the docker-compose version to be used

### SERVICES
```
services:
	container1:
		image:
		volume:
		...
	container2:
	...
```
- Parent command before listing child containers

#### IMAGES
`image: {imageName}`
- command to specify the image to use in the container

#### BUILD
```
build: {path/to/Dockerfile}

or

build:
	context: {path/to/Dockerfile}
	dockerfile: {nameOfDockerfile}
	args:
		arg1: value
		arg2: value
		...
```
- command to specify the dockerfile to build when not working from a finished image
- args is optional.

#### CONTAINER_NAME
`container_name: {containerName}`
- sets the name of the parent container

#### VOLUMES
```
volume:
	- {path/name}:{containerPath}
	- ...
```
- attach volumes to the container

#### PORTS
```
ports:
	- {externalport}:{internalport}
	- ...
```
- command to publish ports
#### ENV
```
enviroment:
	- KEY=Value
	or
	KEY: Value
```
- setting env variable for the container
```
env_file:
	- {path/to/file}
```
- setting path to env file for container

#### NETWORK
```
networks:
	- {networkName}
```
- to specify the network to run the container in
- *****Not nessesary cause all containers in the docker-compose will run on its own network automatically****

### VOLUMES
```
volumes:
	{namedVolume1}:
	{namedVolume2}:
	...
```
- named volumes are to be listed in the syntax above so that docker can keep track
- anonymous volumes or bind mounts do not need to be specified here

#### DEPENDS_ON
```
depends_on:
	- {dependency}
	- ...
```
- command to set dependencies for the container

### INTERACTIVE MODE
```
stdin_open: true
tty: true
```
- commands to start container in interactive mode

### NOTES
- containers are always in detached mode and will be removed automatically


# HOW TO UP/DOWN DOCKER COMPOSE
### UP
`docker compose up`
- command to run the docker compose file
- make sure cli is in the same directory as the docker compose file
- `-d`  - flag to run in detached mode
- `--build` - use to force build images

### DOWN
`docker compose down`
- command to stop the docker compose file
- removes all containers & network
- does not delete volumes
- `-v` - use this flag to remove volumes

### RUN
`docker compose run {serviceName} {Command}`
- command to run only the specified composed service
- optional commands can be added at the end
- does not auto remove container when stopped
	- use `--rm`  to auto delete container