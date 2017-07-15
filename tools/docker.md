# docker
* Dockerhub: registry for collections of images (like npm)
* Image: standalone executable package with all the dependencies needed to run a piece of software
* Container: A runtime instance of an image
	- Containers run natively on a host machine but are isolated from the host
	- containers need to be pre-configured to access files / ports
	- containers can share a single kernel
	- the executable and dependencies do not need to be installed on the host machine
	- CI/CD can push updates to a single part of a distributed application
* Service: defines how a container behaves in production, a service is a part of an application
	- A service runs one image, scaling the service changes the number of container instances running that piece of software
	- docker-compose files can be used to scale a service
* Applications join togethor multiple machines into a 'dockerized' cluseter called a swarm
	- a swarm is a group of machines running docker that have been joined into a cluster
	- machines in a cluster (physical or virtual) are called nodes
	- swarm managers are the only machines that can execute commands, or add new workers
	- workers are machines that provide capacity
* Stack: defines interactions of all the services
* Dockerfile: A portable image defining dependencies
* Networks can be created to manage communication between containers
	- networks isolate your containers
	- by default, containers are created in the **bridge** network
	- a bridge network is limited to a single host running docker engine
	- an **overlay** network can contain multiple hosts
	- a container can be attached to as many networks as you like

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
- `docker stack ls` - list all running applications on this docker host
- `docker stack deploy -c <docker-compose-config> <appname>`
- `docker stack ps <appname>` - show all processes for a stack
- `docker stack rm <appname>` - remove the stack we created
- `docker swarm init` - initialise a swarm, sets the machine as the swarm manager
- `docker swarm join` - join the swarm as a worker
- `docker-machine` - helps manage VMs
- `docker-machine ssh` - allows a swarm manager to send commands to a worker

## Dockerfile commands
* `FROM` - define the base image we are building from, needs to be the first line of your Dockerfile, images are found on dockerhub.
* `WORKDIR` - set the working directory within the container
* `ADD` - copy from current directory into the container directory
* `RUN` - run a command inside the container
* `ENV` - define environemnt variables
* `CMD` - execute a command

## Docker compose
* Specifies tasks that occur both for building images and also running containers
	- it will trigger builds for our images
	- it will populate runtime data such as envvars and volumes

## Links
* [dockerize node apps](https://buddy.works/guides/how-dockerize-node-application)
* [Docker compose for node](https://blog.codeship.com/using-docker-compose-for-nodejs-development/)
* [Automated nginx reverse proxy](http://jasonwilder.com/blog/2014/03/25/automated-nginx-reverse-proxy-for-docker/)
* [Set up docker on your VPS](http://blog.ssdnodes.com/blog/tutorial-getting-started-with-docker-on-your-vps)
* [Docker nginx reverse proxy](http://blog.ssdnodes.com/blog/tutorial-using-docker-and-nginx-to-host-multiple-websites)
