# docker
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

## Dockerfile commands
* `FROM` - define the base image we are building from, needs to be the first line of your Dockerfile, images are found on dockerhub.
* `WORKDIR` - set the working directory within the container
* `ADD` - copy from current directory into the container directory
* `RUN` - run a command inside the container
* `ENV` - define environemnt variables
* `CMD` - execute a command

## Links
* [dockerize node apps](https://buddy.works/guides/how-dockerize-node-application)
