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
`FROM {imageName}:{tag}`
install base image

### WORKDIR
`WOKRDIR {/path}`
Sets root directory for image

### COPY
`COPY {arg1} {arg2}`
arg 1 - copy from source directory (Dockerfile's original directory)
arg 2 - copy to destination in the image (Working Directory set usually /app)

### RUN
`RUN {Commands}`
runs commands in the image's cli, root folder 
runs when image is being built

### ARG
`ARG {key}={value}`
- Set arguments to be used in the Dockerfile
- careful placement of this layer for optimal build

### ENV
`ENV {key} {value}`
- Set enviroment key pair values

### EXPOSE
`EXPOSE {PortNo.}`
Exposes the api's PORT to be used outside the container

### VOLUME
`VOLUME ["{path/in/container}"]`
- adds an anonymous volume to your container

### CMD
`CMD ["{CMD1}", "{CMD2}"]`
- runs when container has started
- syntax - `["{CMD1}", "{CMD2}"]`, eg. `["go", "run", "main.go"]`

---

# HOW TO BUILD/RUN/STOP DOCKER CONTAINER
### DOCKER BUILD
`docker build {path/to/Dockerfile}`
cli command to build the image from your Dockerfile
 - runs in your current directory
 - caches build
 - images will have to be rebuilt when changes to the source code are made
flags
- `-t` adds name:tag to image

### DOCKER RUN
`docker run {flags} {image ID/image Name}`
starts up a container of the specified image given
 - `-p {externalPortNo.:internalPortNo.}` flag binds internal exposed port to the container's external port
 - `-d` flag runs container in background (detached)
 - `-i` flag to run interactive container
 - `-t` flag to run with terminal
 - `--rm` flag to remove container on stop
 - `--name` flag to name container
 - `-v {localName}:{path/in/container}` flag to add named volume to container
 - `--env {key}={value}`  or `-e {key}={value}` flag to set env variables on run
	 - specify multiple env variables with multiple flags
 - `--env-file {path/to/.env/file}` flag to point to app's.env .env file
 - `--build-arg {key}={value}` flag to change build arguments on run
 - `--network {networkName}` flag when running a container to set the container's network

### DOCKER STOP
`docker stop {container name}`
stops the specified docker container

---

# HOW TO COPY FILES INTO / FROM A CONTAINER
`docker cp {arg1} {arg2}` 
- command to copy files to and from a container
	- arg1 - path of the source directory
	- arg2 - containerName:path of the destination

---

# HOW TO PUSH/PULL IMAGES TO DOCKER HUB/PRIVATE REGISTRY

1. Create an account on docker.com and sign in on docker desktop
2. Create new repo on hub.docker.com
3. Use command `docker tag`  to rename image into this format {userName}/{reponame}

### PUSH IMAGE
`docker push {username}/{reponame}:{Image_name}`
- pushes specified image to docker hub
`docker push {Host}:{Image_name}`
- pushes specified image to private registry. `{Host}` is the name of registry

### PULL IMAGE
`docker pull {username}/{reponame}:{Image_name}`
- pulls specified image from docker hub
`docker pull {Host}:{Image_name}`
- pulls specified image from private registry. `{Host}` is the name of registry

---

# NOTES
- images will have to be rebuilt when changes to the source code are made
- use `--help` to check commands

---
