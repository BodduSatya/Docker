*docker pull <image-name>
- pull the docker image from public repository  like doker-hub.

*docker run <image-name> 
- pull & start the image in the container

* docker run -d -p<host-port>:<container-port> -<image-name>
-d : ditached mode.
-name: name of the container
-host-port: system port.
-one host or system may have multiple containers.Each container have one port. we can map host-port to container-port using -p option

eg: docker run -d -p6000:6379 redis:4.0

* docker images
- shows all the images in the host.

* docker run <image-name>
- to create the container with given image & start the container.

* docker start <container-id/container-name>
- start the container

* docker stop <container-id/container-name>
- stop the container

* docker ps
- lists all the running containers

* docker ps -a
- lists all the containers

## Docker Container logging 
* docker logs <container-id/container-name>

## naming the container
 docker run -d  -p6001:6379 --name <custom-name(our-choice)>

## Docker Container Debugging:
* docker exce -it <container-id/container-name> /bin/bash

-it: interactive terminal
-above command will open the interactive terminal, in that u can use following commands
ls
env
exit

*docker network ls
* docker network create <network-name>
* docker run -d \
 -p <host-port>:<container-port>  \ 
 -e <environment-variable-name>  \
 -e <environment-variable-name> \
 --name <container-name> \
 --net <network-name> \
 <image-name>
 
 ## example:
## docker run command
docker run -d \
--name mongo-express \
-p 8080:8080 \

-e ME_CONFIG_MONGODB_ADMINUSERNAME=admin \
-e ME_CONFIG_MONGODB_ADMINPASSWORD=password \
-e ME_CONFIG_MONGODB_SERVER=mongodb \

--net mongo-network \
mongo-express

## mongo-docker-compose.yaml

version:'3'
services:
	mongodb:
		image:mongo
	mongo-express:
		image:mongo-express
		ports:
			-8080:8080
		environment:
			-ME_CONFIG_MONGODB_ADMINUSERNAME:admin
			...
			
## Docker Compose takes care of creating a common network!, no need to specify in docker compose.

## to start the docker script from docker compose
docker-compose -f mongo.yaml up

## to stop the docker script from docker compose
docker-compose -f mongo.yaml down

## display docker list of docker networks
docker network  ls

##docker file is the blueprint for building the image.

## create docker image
docker build -t my-app:1.0 .

## delete container
docker rm <container-name>

## delete image
docker rmi <image-name>
