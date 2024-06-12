# Docker
## Introduction
### Why Docker?
- Let us assume that we are developing an application, and every application has Frontend, Backend and database
- To overcome the above monolithic architecture, we’re using “Docker”
- So while creating the application we need to install the dependencies to run the code
So, I installed Java11, reactJS and MongoDB to run the code. After sometime, I need another version of java, react and MongoDB for my application to run the code
- So, it’s really a hectic situation to maintain multiple versions of same tool in our system
- To overcome this problem, we will use “Virtualization”

## Docker

![Docker Architecture](https://docs.docker.com/get-started/images/docker-architecture.webp)

- It is an open source centralized platform designed to create, deploy and run applications. 
- Docker is written in the GO language.
- Docker uses containers on host OS to run applications. 
- It allows applications to use the same linux kernel as system on the host computer, rather than creating a whole virtual OS.
- Docker is platform independent. i.e. we can install docker on any OS but the “docker engine” runs natively on “Linux” distribution
- Docker performs OS level virtualization also known as containerization
- Before Docker, many users face problems that a particular code is running in the developers system but not in the user system
- Docker is a set of PAAS that use OS level virtualization, where as VMware uses hardware level virtualization 
- Container have OS files but it’s negligible in size compared to original files of that OS

### Docker components

1. **Docker Client**
- It is a primary way that many docker users interact with docker. 
- When you use commands such as docker run, the client sends these commands to docker daemon, which carries them out
- The docker commands uses the docker API
- Overall, here we perform the commands

2. **Docker Host**
- It contains containers, images, volumes, networks
- It is also a server, where we install the docker in a system

3. **Docker Daemon**
- Docker daemon runs on the host OS.
- It is responsible for running containers to manage docker services
- Docker daemon communicates with other daemons
- It offers various docker objects such as images, containers, networking and storage

4. **Docker Registry**
- A Docker registry is a scalable open-source storage and distribution system for docker images
- It is used for storing and sharing the images
- Eg: For git we had GitHub. Same like for docker we had Docker registry

### Comman docker commands
https://github.com/devops-cheat-sheets/kubernetes-docker-cheat-sheet/blob/main/README.md


Command | Explanation
--------|-------------
`docker run image` | Run a Docker container from an image.
`docker run -it image` | Run an image in interactive mode with a terminal attached.
`docker run -d image` | Run an image in the background (detached mode).
`docker run -p 8080:80 image` | Run an image and map host port 8080 to container port 80.
`docker run -v /host/dir:/container/dir image` | Run an image with a host directory mounted into the container.
`docker ps` | List all running Docker containers.
`docker ps -a` | List all Docker containers, both running and stopped.
`docker stop container_id` | Stop a running Docker container.
`docker rm container_id` | Remove a Docker container.
`docker rmi image` | Remove a Docker image.
`docker images` | List all Docker images.
`docker pull image` | Pull a Docker image from a registry.
`docker push image` | Push a Docker image to a registry.
`docker build -t image .` | Build a Docker image from a Dockerfile in the current directory.
`docker exec -it container_id command` | Execute a command in a running Docker container.
`docker logs container_id` | Get the logs from a Docker container.
`docker network ls` | List all Docker networks.
`docker volume ls` | List all Docker volumes.
`docker login` | Log in to a Docker registry.
`docker tag image new_tag` | Tag a Docker image with a new tag.
`docker history image` | Show the history of an image, including the commands that were run to build it.
`docker inspect container_id` | Display detailed information in JSON format for a running container.
`docker search term` | Search the Docker Hub for images.
`docker save -o file.tar image` | Save an image to a tar archive.
`docker load -i file.tar` | Load an image from a tar archive.
`docker top container_id` | Display the running processes in a container.
`docker diff container_id` | Show file system changes in a container.
`docker cp container_id:/file/path /host/path` | Copy files/folders from a container to the host.
`docker commit container_id new_image` | Create a new image from a container's changes.
`docker port container_id` | Show port mapping for a container.
`docker stats container_id` | Show a live stream of container(s) resource usage statistics.
`docker wait container_id` | Block until a container stops, then print its exit code.
`docker update container_id` | Update configuration of one or more containers.
`docker system df` | Display detailed information on space usage within Docker.
`docker system prune` | Remove all unused Docker objects.
`docker container ls` | List all running containers. Similar to `docker ps`.
`docker container rm container_id` | Remove one or more containers. Similar to `docker rm`.
`docker image ls` | List all images. Similar to `docker images`.
`docker image rm image_id` | Remove one or more images. Similar to `docker rmi`.
`docker network create network_name` | Create a new network.
`docker volume create volume_name` | Create a new volume.
`docker network connect network_name container_id` | Connect a network to a container.
`docker network disconnect network_name container_id` | Disconnect a network from a container.
`docker volume inspect volume_name` | Display detailed information on a specific volume.
`docker image inspect image_name` | Display detailed information on a specific image.
`docker container start container_id` | Start one or more stopped containers.
`docker container stop container_id` | Stop one or more running containers.
`docker container pause container_id` | Pause all processes within one or more containers.
`docker container unpause container_id` | Unpause all processes within one or more containers.
`docker container restart container_id` | Restart one or more containers.
`docker container kill container_id` | Kill one or more running containers.
`docker container attach container_id` | Attach local standard input, output, and error streams to a running container.
`docker container prune` | Remove all stopped containers.
`docker image prune` | Remove unused images.
`docker container export container_id -o file.tar` | Export a container's filesystem as a tar archive.
`docker container commit container_id` | Create a new image from a container's changes.
`docker container rename old_name new_name` | Rename a container.
`docker container run -it --rm --name container_name image` | Run a command in a new container, interactively, remove the container when it stops, and name it.
`docker container exec -it container_id command` | Run a command in a running container, interactively.
`docker buildx build --platform linux/amd64,linux/arm64 -t image .` | Build an image for multiple platforms using buildx.
`docker buildx ls` | List builder instances.
`docker buildx use builder_name` | Set the current builder instance.
`docker buildx create --use` | Create a new builder instance and switch to it.
`docker buildx inspect --bootstrap` | Inspect current builder instance.
`docker buildx rm builder_name` | Remove a builder instance.
`docker secret create secret_name secret_data` | Create a secret from a file or STDIN as a single string.
`docker secret rm secret_name` | Remove one or more secrets.
`docker service create --name service_name image` | Create a new service.
`docker service ls` | List services.
`docker service rm service_name` | Remove one or more services.
`docker service scale service_name=num_replicas` | Scale one or multiple replicated services.
`docker service update service_name` | Update a service.
`docker service ps service_name` | List the tasks of one or more services.
`docker service logs service_name` | Fetch the logs of a service or task.
`docker config ls` | List configs.
`docker config create config_name file` | Create a config from a file or STDIN.
`docker config rm config_name` | Remove one or more configs.
`docker plugin ls` | List plugins.
`docker plugin install plugin_name` | Install a plugin.
`docker plugin rm plugin_name` | Remove one or more plugins.
`docker plugin enable plugin_name` | Enable a plugin.
`docker plugin disable plugin_name` | Disable a plugin.
`docker checkpoint ls container_id` | List checkpoints.
`docker checkpoint create container_id checkpoint_name` | Create a checkpoint.
`docker checkpoint rm container_id checkpoint_name` | Remove a checkpoint.
`docker system info` | Display system-wide information.
`docker system events` | Get real time events from the server.
`docker trust signer add --key signer_pub_key.pem signer_name repo/image` | Add a signer for a repository or image.
`docker trust revoke repo/image` | Revoke a signed tag.
`docker trust inspect --pretty repo/image` | Return detailed information about signatures for images.
`docker login [options] [server]` | Log in to a Docker registry server.
`docker logout [server]` | Log out from a Docker registry server.
`docker manifest create list image[:tag] [image[:tag] ...]` | Create a local manifest list for annotating and pushing to a registry.
`docker manifest inspect image[:tag]` | Display an image's manifest, or a local or remote manifest list.
`docker manifest push [options] name[:tag]` | Push a manifest list or image index to a registry.
`docker manifest annotate name[:tag] image[:tag] [options]` | Add additional information to a local image manifest or manifest list.
`docker network prune` | Remove all unused networks.
`docker volume prune` | Remove all unused volumes.
`docker image save image -o file.tar` | Save one or more images to a tar archive.
`docker image load -i file.tar` | Load an image or repository from a tar archive.
`docker image prune -a` | Remove all unused images, not just dangling ones.
`docker container port container_id` | List port mappings for the container, or specify a specific mapping.
`docker container diff container_id` | Inspect changes to files or directories on a container's filesystem.
`docker container top container_id` | Display the running processes of a container.
`docker container stats [container_id...]` | Display a live stream of container(s) resource usage statistics.
`docker container exec -it container_id command` | Run a command in a running container.
`docker network create -d driver_name network_name` | Create a network with a specified driver.
`docker network rm network_id` | Remove one or more networks.
`docker network connect network_id container_id` | Connect a network to a container.
`docker network disconnect network_id container_id` | Disconnect a network from a container.
`docker volume create volume_name` | Create a volume.
`docker volume rm volume_name` | Remove one or more volumes.
`docker volume inspect volume_name` | Display detailed information on a specific volume.
`docker volume prune` | Remove all unused local volumes.
#### check docker version
```bash
docker --version
docker version
```
#### To check state of docker server
```bash
docker info
docker # give commands to use with docker
docker <command> --help
```
#### Docker search on DockerHUB

```bash
docker search <image-name>
```
#### Pull the image from GITHub
```bash
docker pull <image-name>
```
#### Chech downloaded/Pulled/created images 
```bash
docker images <image-name>
```
#### Create container from image with foreground
- `-t` terminal
- `-i` interactive mode
- `-d` detach mode

```bash
docker container run -it --name containe1 nginx
```

#### Create container from image with foreground+background
```bash
docker container run -itd --name containe1 nginx
```
#### Create container from image with foreground+background and expose port
```bash
docker run -itd -p 4000:80 containe1 nginx 
```
#### See a list of all/running containers
```bash
docker ps  # Old way
docker container ls
docker ps -a 
docker container ls -a
```
#### containar administration 
```bash
docker start <hash> # start the container followed by ID
docker stop <hash> # Gracefully stop the specified container
docker kill <hash> # Force shutdown of the specified container
```
####  Enter a running container
```bash
docker exec -it [container-id] bash 
```

#### 
```bash
docker inspect containerName  # inspect we can see the container full information like source code
docker logs <container-id> -f               # Live tail a container's logs

```
#### Remove the specified container or image
```bash
docker rm <hash>                            # Remove the specified container from this machine
docker rm -f <hash>                         # Remove force specified container from this machine
docker rm $(docker ps -a -q)                # Remove all containers from this machine

docker rmi <imagename>                      # Remove the specified image from this machine
docker rmi $(docker images -q)              # Remove all images from this machine
```
#### Remove all unused resources
```bash
docker system prune   # Remove all unused containers, networks, images (both dangling and unreferenced), and optionally, volumes. (Docker 17.06.1-ce and superior)
docker volume prune   # Remove all unused local volumes
docker network prune  # Remove all unused networks
```

```bash
docker run -m 4m -dit --name web1 nginx   # running the container with a limit of 4mb
docker container inspect local_registry  #Inspect the container
```

## docker save and load command
```bash
docker save mywebserver > mywebserver.tar
docker load < mywebserver.tar
```

## Docker image build
### 1. Container to Image Creation

- we create the container through the image. But, right now we're creating the image through the running container.
- In above diagram, we're creating the container from nginx image. So, we need the same container again. Generally, we're creating another image and we created the container
- But, Instead of above process. Here, In container already files are present. So, if we create the image from that container. We will get the same files in that image
- Now, Instead of creating the separate container. Already, through Httpd image if we run means that all files directly came to another container.
- i.e. automatically same application deployed

```bash
docker commit containerName NewImageName # Create the image from the container
docker commit cont1 httpd #Check the images
docker images
```
- Through that image create the container

```bash
docker run -itd --name cont2 -p 8085:80 httpd
```

### 2. Dockerfile

- It is basically a text file which contains set of instructions (or) commands To create the docker images, we're using Docker file
- Here, we're not having multiple Docker files i.e. For single directory we're having single Docker file In Docker file the first letter should be `D`
- In Docker file we're having components And start components also be capital letter

- Docker can build images automatically by reading the instructions from a `Dockerfile`.
- A Dockerfile is text document that contains all the commands a user could call on the command line to assemble an image
- A docker images consists of read-only layers each of which represents a `Dockerfile` instruction
- Command to build image from Dockerfile. `docker build -f <path of docker file>`


### Docker file instructions

**FROM** 
- FROM is define the base image on which we are building
- A valid Docker must start with a `FROM` instructions  
- Format:
 FROM <image>:<tag>

**LABEL	(or) MAINTAINER**
- LABEL added to image to organize images by project, record licensing information or Author details.
- For each label, add a line begining with LABEL and with one or more key-value pair.
- Format:
  LABEL vender1="0.1-beta"

**RUN**
- RUN is used to add layers to the base image, by installing components.
- Each RUN statement add a new layer to the docker image
- The resulting commited image will be used for the next step in the `Dockerfile`
- Format:
        RUN apt-get update
        RUN apt-get -y install apache2

**CMD** 
- CMD instruction should be used to run the software contained by your image, along with any arguments.
- There can only be one CMD instruction in a Dockerfile. If ou list more then one CMD then only the last CMD will take effect.
- The main purpose of a CMD is to provide defaults for an executing container.
- Format
  CMD apachectl -D FOREGROUND

**EXPOSE**
- EXPOSE instruction indicates the ports on which a container listens for connections.
- Format:
  EXPOSE <port>

**ENV** 
- ENV is used to define the environment variable in container
- ENV name Devops 

**ADD** 
- ADD instructions copies new files, directories or remote URLs from <source> adds them to the filesystem of image at path <destination> in the container. 
- ADD <source> <destination in the container>
- ADD index.html /var/www/html

**COPY**
Same as 'ADD', but without the tar and remote URL handling.

**VOLUME**
- VOLUME instruction should be used to expose any database storage area, configuration storage, or files/folder created by your docker container.

**WORKDIR**
- WORKDIR instruction sets the working diectory for any RUN, CMD, ADD instructions that follow it in Dockerfile.
- Format
  WORKDIR $PATH

**ENTRYPOINT**
- is used to strictly run the commands the moment the container intializes. 
- The differnece between CMD and ENTRYPOINT is, ENTRYPOINT runs irrespective of the fact that whether argument is specified or not
			ENTRYPOINT apachectl -D FOREGROUND

#
- In this Dockerfile , the ENTRYPOINT directive specifies the default command that will get executed when a container is run from the custom Docker image. The CMD directive, on the other hand, provides the default argument for the `ENTRYPOINT` directive.



## Project:- Java jenkins tomcat

- Create a docker file Dockerfile
**Example-1**
```bash
FROM ubuntu
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update
RUN apt-get -y install apache2
ADD . /var/www/html
ENTRYPOINT apachectl -D FOREGROUND
ENV name DEVOPS 
```

**Example-2**
```bash
FROM centos:7 # Base image is CentOS 7
# Add a new user "john" with user id 8877
RUN useradd -u 8877 john
# Change to non-root privilege
USER john
```

```bash
sudo docker build -t nonrootimage . # create custom image
docker exec -it test2 bash
```

### Eample of COPY and ADD
```bash
FROM centos:7.4.1708
RUN mkdir /mydata
COPY myfiles /mydata/myfiles
ADD myfiles2 /mydata/myfile2
ADD https://xxx/pip-18.1.tar.gz /mydata
ADD pip-18.1.tar.gz /mydata/pipunpack
```

### CMD and ENTRYPOINT
```bash
FROM ubuntu
CMD echo "Hello World"
```
```bash
docker build . -t  img1   #Created the image from above Dockerfile
docker run -it img1 # it will return Hello World
docker run -it img1 echo "Hello India" # it will overwrite the CMD and Print Hello India
```
```bash
FROM ubuntu
ENTRYPOINT ["echo","Hello World"]
```

```bash
docker build . -t  img1   #Created the image from above Dockerfile
docker run -it img1 # it will return Hello World
docker run -it img1 echo "Hello India" # it will not overwrite the ENTRYPOINT and Print Hello World echo Hello India
```

```bash
FROM ubuntu
ENTRYPOINT ["echo"]
CMD ["Hello World"]
```

```bash
docker build . -t  img1   #Created the image from above Dockerfile
docker run -it img1 # it will return Hello World
docker build . -f abc -t img8 # abc is the file name which represents the dockerfile contents
```
 
## Apply Tags in Images

- If we don't want to overriding the image. i.e. I want to see the same name for old image and new image. Without overriding
- Because, if we creating image with same name that image will override. 
- So, we lose that data. So, if we use tags means our image will not override
- Almost, we will use tags when we build a Dockerfile Command is:

```bash
docker build -t image:1 . 
docker build -t image1:2 .
```

## Docker Storage
- Data will removed if container is deleted. so, docker storage is used to keep the data even if container is deleted.

### Types of Docker Storage:

#### Docker Volume 
- is a mountable entity which can be used to store data, in the docker file system
```bash
docker volume  create my-vol
```

- it is software not the hardware component it can be attached and deattached
```bash
docker volume create demo-vol
docker volume ls     # to list the volumes
docker run -it --mount source=demo-vol,destination=/app -d ubuntu
docker run -it --mount source=demo-vol,destination=/test -d ubuntu

```
- remove the container
- attach volume to another container

#### Bind Mounts
- mounts a directory from host machine to the container
- To mount the directory which on the host machine to container

```bash
docker run -it -v /home/ubuntu/mount:/demo -d ubuntu
```

#### Linking docker Containers
- run container with name
```bash
docker run -itd --name container1 ubuntu
docker run -itd  --name container3 --link container1 ubuntu
```
 
## Docker Network
bridge(default) :- When the application is running in the standalone container that need to communicate
host :- For standalone containers, remove network isolation between container and docker host and use host networking directly (not port forwrading)
overlay:-connect multiple docker demons and enable swarm service to communicate with each other
MacVlan:-allow you to assign a MAC network address to a container to appear as a physical machine.
none:-disable networking


- List network
```bash
docker network ls
Create the network
docker network create -d overlay my-overlay

```

## Docker-HUB

- Create a Docker Hub account (https://hub.docker.com)
- create a user defined images

```bash
docker commit <<container id>> <<new image name>>   // example we have created test image
docker images
```
- run docker new image and check the changes should be available into that
- push image to docker hub

```bash
 docker login
 docker push ramansharma95/apache
```
- check in the docker hub
   
## Create Local Docker registry
```bash
docker container run -d -p 5000:5000 --name local_registry registry
http://<serverip>:5000/v2/_catalog
```
```bash
docker container inspect local_registry
docker image tag ubuntu localhost:5000/ubuntu:latest
docker image push localhost:5000/ubuntu
docker image pull localhost:5000/ubuntu
```

## Compose file

```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.23.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
docker-compose --version
```
- YAML
- It is superset of Json file. There are 2 types of component you need to learn 
- Map:-key value pair <key>:<value>   eg Name:Devops
- List:-Sequences of objects
- args
  -sleep
  -"1000"

#### Create a compose file to run db and we app ( file name should be docker-compose.yml)
```bash

version: '3.3'

services:
   db:
      image: ramansharma95/mysql
   web:
      depends_on:
      - db
      image: ramansharma95/webapp
 
 To execute compose file
 docker-compose up -d
 To remove the services for docker compose
 docker-compose down
``` 
## Interview Que

### Are you able to remove a paused container in Docker?
- No, you cannot remove any paused docker container. You can only remove a container when it is in the stopped state.

### Can a container get automatically restart?
- By default, the flag restart remains false. So, it is not possible for a container to automatically restart.

### Is it good if you run stateful applications over Docker?
- The concept of statement applications says that their data gets stored on the local file system. 
- So, when you move the application to another device, it will become difficult for you to retrieve data. 
- So, we do not recommend running stateful applications here.


### What is a .dockerignore file?
- we also have a Dockerignore files which allows you to mention a list of files and/or directories which you might want to ignore while building the image

### What is a Docker Namespace?
- https://www.youtube.com/watch?v=Z7swPxOeRzM&list=PLOwc7JW6aCQFUrd5uOsLKIvWI_q-ghblc

- A namespace is one of the Linux features and an important concept of containers. 
- Namespace adds a layer of isolation in containers. 
- Docker provides various namespaces in order to stay portable and not affect the underlying host system. 
- Few namespace types supported by Docker — PID, Mount, IPC, User, Network
- We can understand on how docker creates containers using Linux features like namespaces and cgroups etc., to build a container for docker to run application.
1) PID namespace
2) Network namespace
3) Mount(mnt) namespace
4) UTS namespace
5) IPC namespace
6) User namespace

- Application uses system calls to Kernel to interact to harware in linux
- os kernel + system calls = kernle space
- Application is user space


```bash
[root@docker ~]# lsns
        NS TYPE  NPROCS   PID USER   COMMAND
4026531836 pid      189     1 root   /usr/lib/systemd/systemd --switched-root --system --deserialize 22
4026531837 user     189     1 root   /usr/lib/systemd/systemd --switched-root --system --deserialize 22
4026531838 uts      189     1 root   /usr/lib/systemd/systemd --switched-root --system --deserialize 22
4026531839 ipc      189     1 root   /usr/lib/systemd/systemd --switched-root --system --deserialize 22
4026531840 mnt      182     1 root   /usr/lib/systemd/systemd --switched-root --system --deserialize 22
4026531856 mnt        1    28 root   kdevtmpfs
4026531956 net      188     1 root   /usr/lib/systemd/systemd --switched-root --system --deserialize 22
4026532183 mnt        1   587 chrony /usr/sbin/chronyd
4026532249 net        1   630 rtkit  /usr/libexec/rtkit-daemon
```
- And on os process of container running is

```bash
[root@docker ~]# lsns -t pid
        NS TYPE NPROCS   PID USER COMMAND
4026531836 pid     190     1 root /usr/lib/systemd/systemd --switched-root --system --deserialize 22
4026532190 pid       2  6918 root sh -c sleep 1d

[root@docker ~]# ps -aux | grep 6918
root      6918  0.1  0.0   2876   772 ?        Ss   16:00   0:00 sh -c sleep 1d
root      6994  0.0  0.0 112808   964 pts/0    S+   16:02   0:00 grep --color=auto 6918

[root@docker ~]# ps -aux | grep sleep
root      6918  0.1  0.0   2876   772 ?        Ss   16:00   0:00 sh -c sleep 1d
root      6939  0.0  0.0   2776   500 ?        S    16:00   0:00 sleep 1d
root      6992  0.0  0.0 108052   356 ?        S    16:01   0:00 sleep 60
root      6997  0.0  0.0 112808   968 pts/0    S+   16:02   0:00 grep --color=auto sleep
[root@docker ~]#
```

- Inside container process ID is 1

```bash
[root@docker ~]# docker exec -ti c1 ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.0   2876   772 ?        Ss   21:00   0:00 sh -c sleep 1d
root         7  0.0  0.0   2776   500 ?        S    21:00   0:00 sleep 1d
root         8  0.0  0.0   7048  1448 pts/0    Rs+  21:04   0:00 ps aux
[root@docker ~]#
```

##  The methods by which we can achieve docker image optimization.

### Using distroless/minimal base images
- Your first focus should be on choosing the right base image with a minimal OS footprint.
- Distroless images are so minimal that they don’t even have a shell in them. 

### Multistage docker file
- The multistage build pattern is evolved from the concept of builder pattern where we use different Dockerfiles for building and packaging the application code. 
- Its reduces nearly `80%` of images size. 
- https://www.youtube.com/watch?v=hmpUegtHG9s
- to run the container required `App`, `Runtime`, `Base OS image` in image. `SRC` and `Build tools` not required in image.

### Minimizing the number of layers
-  Docker images work in the following way – each `RUN`, `COPY`, `FROM` Dockerfile instructions add a new layer & each layer adds to the build execution time & increases the storage requirements of the image.
- Using this optimization technique, the execution time was reduced from `117.1s` to `91.7s` & the storage size was reduced from `227MBs` to `216MBs.`

### Understanding caching
- Due to this concept, it’s recommended to add the lines which are used for installing dependencies & packages earlier inside the Dockerfile – before the `COPY` commands.
- The reason behind this is that docker would be able to cache the image with the required dependencies, and this cache can then be used in the following builds when the code gets modified.

### Using Dockerignore
- Docker can ignore the files present in the working directory if configured in the .dockerignore file.

### Keeping application data elsewhere
- Storing application data in the image will unnecessarily increase the size of the images.
- It’s highly recommended to use the volume feature of the container runtimes to keep the image separate from the data.

### Dive tool for optimization
https://github.com/wagoodman/dive

