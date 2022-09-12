# DATA?
- Application data
	- the code written by the developer
	- added to image and container in build phase
	- is read-only once image is built
- Temp App Data
	- Fetched/Produced in running container
	- Stored in memory or temp files
	- Dynamic and changing
	- Stored in containers
	- eg. user input
- Permanent App Data
	- eg. user accounts
	- fetched / produced in running container
	- stored in files or database
	- must be persistant
	- use of volumes

# VOLUMES
- folders on your host machine which are mounted into containers
- persistant data
- A container can read or write data into a volume

### Anonymous Volumes
- is not persistant
	- only exists when container is up
- is automatically removed when a container is tagged with  `--rm`

### Named volumes
- `-v {nameOfVolume}:{path/in/container}` flag to add named volume to container
- is persistant but should not be edited by user

# BIND MOUNTS
- `-v {absolute/path/to/local/code}:/{workingDir/in/container}`
- `-v $(pwd):/{workingDir/in/container}` short cut to path - mac
- `-v "%cd%":/{workingDir/in/container}` shortcut to path - windows
- User defines a folder / path on host machine
- persistant and editable data
- MAKE SURE DIRECTORY IS ACCESSIBLE TO DOCKER
	- docker preferences
		- file sharing
- use with anonymous volume if there are clashes
	- if there is a clash, longest internal path wins