# CONTAINER vs IMAGE

## Containers
The running unit of software
- running instance of Images
- container based on image as a layer
	- layers are cached on build

## Images
- images hold the code
-  blueprint/template of the application
- layer base architecture

---

# HOW TO BUILD A DOCKERFILE

### FROM
install base image

### WORKDIR
Sets root directory for image

### COPY
`COPY {arg1} {arg2}`
arg 1 - copy from source directory (Dockerfile's original directory)
arg 2 - copy to destination in the image (Working Directory set usually /app)

### RUN
runs commands in the image's cli, root folder 
runs when image is being built

### EXPOSE
Exposes the api's PORT to be used outside the container

### CMD
- runs when container has started
- syntax - ["{CMD1}", "{CMD2}"], eg. ["go", "run", "main.go"]

---

# HOW TO RUN/STOP DOCKER CONTAINER
### Docker Build
`docker build {path/to/Dockerfile}`
cli command to build the image from your Dockerfile
 - runs in your current directory
 - caches build
 - images will have to be rebuilt when changes to the source code are made

### Docker run
`docker run -p {externalPortNo.:internalPortNo.} {image ID/image Name}`
starts up a container of the specified image given
 - `-p` flag binds internal exposed port to the container's external port
 - `-d` flag runs container in background (detached)
 - `-i` flag to run interactive container
 - `-t` flag to run with terminal
 - `--rm` flag to remove container on stop

### DOCKER STOP
`docker stop {container name}`
stops the specified docker container

---

# HOW TO COPY FILES INTO / FROM A CONTAINER
`docker cp {arg1} {arg2}`
- command to copy files to and from a container
	- arg1 - path of the source directory
	- arg2 - path of the destination

---

# NOTES
- images will have to be rebuilt when changes to the source code are made
- use --help to check commands

---

# DOCKER COMMANDS
### ATTACH
`docker attach {containerid/name}`
- attaches to a running detached container

### LOGS
`docker logs {containerID/name}`
- shows the logs for a running container

### RM
`docker rm {containerID/Name}`
- removes containers

### IMAGES
`docker images`
- list images

### RMI
`docker rmi {imageID/Name}`
- removes images
- can only remove when not used by a container
	- remove child containers first!

### PRUNE
`docker image prune`
- remove unused/dangling images
`docker container prune`
- remove stopped containers

### DOCKER STOP
`docker stop {container name}`
stops the specified docker container

### DOCKER PS
`docker ps`
command to list containers

### INSPECT
`docker image inspect {imageID/Name}`
- Display detailed information on one or more images
`docker container inspect {containerID/Name}`
- Display detailed information on one or more containers

### CP - COPY
[[#HOW TO COPY FILES INTO FROM A CONTAINER]]
`docker cp {arg1} {arg2}` 
- command to copy files to and from a container
	- arg1 - path of the source directory
	- arg2 - path of the destination



---
