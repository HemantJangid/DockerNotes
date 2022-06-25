# DOCKER

Read basics from this link
https://medium.com/@kmdkhadeer/docker-get-started-9aa7ee662cea#:~:text=Docker%20is%20a%20set%20of,other%20through%20well%2Ddefined%20channels.

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
