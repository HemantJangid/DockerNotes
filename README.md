# DOCKER

Read basics from this link
https://medium.com/@kmdkhadeer/docker-get-started-9aa7ee662cea#:~:text=Docker%20is%20a%20set%20of,other%20through%20well%2Ddefined%20channels.

### DOCKER CHEAT SHEET

https://www.docker.com/wp-content/uploads/2022/03/docker-cheat-sheet.pdf

## DOCKER COMMANDS

### BASIC COMMANDS

- `docker command options container_name` basic commmand structure
- `docker version` gets current version of docker and info
- `docker pull image_name` get provided image from docker hub
- `docker pull image_name:version_number` get provided image of particular version from docker hub
- `docker run image_name` runs the provided image
- `docker run -d image_name` runs the provided image in detached mode
- `docker ps` lists all running docker containers
- `docker ps -a` lists all containers wheather running or not running
- `docker images` lists all available docker images
- `docker stop container_id` stops the provided container
- `docker start container_id` starts the provided container
- `docker run -p6000:6379 redis` runs the redis container and binds it to the 6000 port of host machine with 6379 port of container
- `docker run -p6000:6379 -d redis` runs the redis container and binds it to the 6000 port of host machine with 6379 port of container in detached mode
- `docker run -p6000:6379 -d --name redis-new redis` creates new container with provided imags of redis and names it "redis-new"

### TROUBLESHOOTING COMMANDS

- `docker logs container_id|container_name` prints logs of the provided container
- `docker exec -it container_id|container_name /bin/bash` gives excess to the terminal for provided container

## DOCKER V/S VIRTUAL MACHINE

https://www.youtube.com/watch?v=5GanJdbHlAA

## NETWORK COMMANDS

- `docker network ls` - list all networks
- `docker network network_name` - create new network with given name

## NODE APP WITH DOCKER

https://www.youtube.com/watch?v=6YisG2GcXaw&list=PLy7NrYWoggjzfAHlUusx2wuDwfCrmJYcs&index=8

when using any images like mongodb, you can pass environment variables as well for username and password, to do that checkout the description of the image you are using to create the conatainer

example -

#### start mongoDb

`docker run -d -p:27017:27017 --network network_name --name container_name -e MONGO_INITDB_ROOT_USERNAME=mongoadmin -e MONGO_INITDB_ROOT_PASSWORD=secret mongo ` network is passed manually to make sure to run different services in same network so they can communicate directly without any need to expose ports

####

`docker run -d -p:27017:27017 --network network_name --name container_name -e ME_CONFIG_MONGODB_ADMINUSERNAME=mongoadmin -e ME_CONFIG_MONGODB_ADMINPASSWORD=secret mongo-express`

## DOCKER COMPOSE

using docker compose we can map the commands that we used earlier to a file which can be further used to create any number of containers using that blueprint

example based on the above commands: this is the whole .yaml file

```
version: '3'
services:               // list all services inside it
    mongodb:                    // container name
        images: mongo                   // image name
        ports:                          // define port bindings
            - 27017:27017
        environment:                    // define environment variables
            - MONGO_INITDB_ROOT_USERNAME=mongoadmin
            - MONGO_INITDB_ROOT_PASSWORD=secret

    mongo-express:
        images: mongo-express
        ports:
            - 8080:8080
        environment:
            - ME_CONFIG_MONGODB_ADMINUSERNAME=mongoadmin
            - ME_CONFIG_MONGODB_ADMINPASSWORD=secret
```

To create container using this

`docker-compose -f filename.yaml up -d` takes filename for yaml name

To stop all the containers

`docker-compose -f filename.yaml down` when stopping container using docker compose it also removes the network it created at the time of creating the containers

## DOCKER FILE

To create the docker image we need to create a dockerfile. It acts an blueprint for creating docker images
example:

```
FROM node           // every image is based on some base image // install node
ENV MONGO_INITDB_ROOT_USERNAME=mongoadmin \             // define environment variables
    MONGO_INITDB_ROOT_PASSWORD=secret
RUN mkdir -p /home/app                              // runs this command on the container shell and creates a /home/app folder
COPY ./home/app                                 // copy current folder files to /home/app // this executes on the host
CMD ["node", "server.js"]                       // entry command to run when container is created successfully
```

This file has to be saved like "Dockerfile" name has to be exact same

`docker build -t image_name:version directory_of_dockerfile` creates image file, takes in a image name, version and location of dockerfile

Note: Whenver you make changes to the dockerfile you need to create a new image after that and create new container

## CREATING PRIVATE REPOSITORY - DOCKER REGISTRY

https://www.youtube.com/watch?v=vWSRWpOPHws&list=PLy7NrYWoggjzfAHlUusx2wuDwfCrmJYcs&index=11

## DOCKER VOLUMES

https://www.youtube.com/watch?v=p2PH_YPCsis&list=PLy7NrYWoggjzfAHlUusx2wuDwfCrmJYcs&index=12
