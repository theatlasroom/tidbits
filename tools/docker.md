# docker
* Dockerhub: registry for collections of images (like npm)
* Image: standalone executable package with all the dependencies needed to run a piece of software
* Container: A runtime instance of an image
	- Containers run natively on a host machine but are isolated from the host
	- containers need to be pre-configured to access files / ports
	- containers can share a single kernel
	- the executable and dependencies do not need to be installed on the host machine
	- CI/CD can push updates to a single part of a distributed application
* Service: defines how a container behaves in production
* Stack: defines interactions of all the services
* Dockerfile: A portable image defining dependencies

## Docker Commands
- `docker ps` - list active processes
	* `-a` - all containers, even the ones not running
- `docker build` - your docker file
	* `-t <name>` - tag the built image with a name
- `docker images` - list all our built images
	* `-a` - all images
- `docker run <image>` - run the app specified by name
	* You can also use the full identifier for a image ie `docker run username/repository:tag`
	* `-p <local-machine-port>:<container-port>` - map your local port to a port inside the container (the one you EXPOSE)
	* `-d` - run in detached (daemon) mode, so the container runs in the background
- `docker stop <container-id>` - stop a container using its container id
- `docker login` - login to your cloud.docker.com account
- `docker kill <container-id>` - forced shutdown of the container
- `docker rm <container-id>` - remove the container specified from this machine
	* `docker rm $(docker ps -a -q)` - remove all containers
-

## Dockerfile commands
* `FROM` - define the base image we are building from, needs to be the first line of your Dockerfile, images are found on dockerhub.
* `WORKDIR` - set the working directory within the container
* `ADD` - copy from current directory into the container directory
* `RUN` - run a command inside the container
* `ENV` - define environemnt variables
* `CMD` - execute a command

## Links
* [dockerize node apps](https://buddy.works/guides/how-dockerize-node-application)
