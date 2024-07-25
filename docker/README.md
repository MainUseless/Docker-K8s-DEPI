# Lab 0

### problem 1

* How do you run a Node.js application using Docker, using the official Node.js image?

  ```
  dockerfile
  =================================
  FROM node:14

  WORKDIR /usr/src/app

  COPY package*.json ./

  RUN npm install

  COPY . .

  EXPOSE 3000

  CMD ["node", "index.js"]

  .dockerignore
  =================================
  node_modules

  command
  =================================
  docker build -t nodejs-app .
  docker run -d --name nodejs-container nodejs-app
  ```
* What command would you use to mount a local directory into a Node.js Docker container?

  ```
  using -v option in the run command

  docker run -d --name nodejs-container -v /localpath:/containerpath nodejs-app
  ```
* What is the command to copy files from your local machine into a running Python Docker containerand vice versa?

  ```
  using cp command

  docker cp /localfilepath <container_name\id>:/containerpath
  ```
* How can you execute a Python script inside a running Docker container?

  ```
  using exec command

  docker exec <container_name\id> python /python/file/path
  ```
* How do you start a Nginx Docker container and expose it on port 80?

  ```
  using -p option <host_port>:<container_port> in run command

  docker run -d --name nginx -p 80:80 nginx
  ```
* What command can you use to inspect the Nginx container's logs?

  ```
  docker logs nginx
  ```
* How can you list all Docker images on your system?

  ```
  docker images
  docker image list
  ```
* What is the purpose of the docker ps command, and how can you see all containers, including stopped ones?

  ```
  The docker ps command is used to list the running containers in your Docker environment. And provides information like container id, image used, the running command inside the container, ...

  To list all containers includion stopped we use the -a option
  docker ps -a
  ```
* How can you stop a running Docker container gracefully?

  ```
  using stop command

  docker stop <container_name\id>
  ```
* What command would you use to remove all stopped containers from your system?

  ```
  using container prune command

  docker container prune
  ```
* How can you view detailed information about a Docker image, including its layers?

  ```
  using the inspect command

  docker inspect <container_name\id>
  ```
* What is the difference between a Docker image and a Docker container, and how do you create a container from an image?

  ```
  A Docker image is a lightweight, stand-alone, and executable software package that includes everything needed to run a piece of software, including the code, runtime, libraries, environment variables, and configuration files.

  Definition: A Docker container is a runtime instance of a Docker image. It includes the Docker image and a writable layer on top, allowing it to run as an isolated process on a host machine.

  To create and run a container from a Docker image, you use the run command. This command not only creates a container from an image but also starts it.

  docker run image-name
  ```


# lab 1

### problem 1

* Run the container hello-world

  ```
  $ docker run hello-world
  Unable to find image 'hello-world:latest' locally
  latest: Pulling from library/hello-world
  c1ec31eb5944: Pulling fs layer
  c1ec31eb5944: Verifying Checksum
  c1ec31eb5944: Download complete
  c1ec31eb5944: Pull complete
  Digest: sha256:1408fec50309afee38f3535383f5b09419e6dc0925bc69891e79d84cc4cdcec6
  Status: Downloaded newer image for hello-world:latest

  Hello from Docker!
  This message shows that your installation appears to be working correctly.
  ...
  ```
* Check the container status

  ```
  $ docker ps -a
  CONTAINER ID   IMAGE         COMMAND    CREATED         STATUS                     PORTS     NAMES
  b510b770725a   hello-world   "/hello"   2 minutes ago   Exited (0) 2 minutes ago             cranky_tesla
  ```
* Start the stopped container

  ```
  $ docker start b510b
  b510b
  ```
* Remove the container

  ```
  $ docker rm b510b
  b510b
  ```
* Remove the image

  ```
  $ docker rmi hello-world
  Untagged: hello-world:latest
  Untagged: hello-world@sha256:1408fec50309afee38f3535383f5b09419e6dc0925bc69891e79d84cc4cdcec6
  Deleted: sha256:d2c94e258dcb3c5ac2798d32e1249e42ef01cba4841c2234249495f87264ac5a
  Deleted: sha256:ac28800ec8bb38d5c35b49d45a6ac4777544941199075dff8c4eb63e093aa81e
  ```


### Problem 2

* docker run -it centos

  ```
  using run command with it option

  $ docker run -it ubuntu
  Unable to find image 'ubuntu:latest' locally
  latest: Pulling from library/ubuntu
  9c704ecd0c69: Pull complete
  Digest: sha256:2e863c44b718727c860746568e1d54afd13b2fa71b160f5cd9058fc436217b30
  Status: Downloaded newer image for ubuntu:latest
  root@7f3ea0c0775a:/#
  ```
* Run the following command in the container “echo docker”

  ```
  root@7f3ea0c0775a:/# echo docker
  docker

  or 

  $ docker exec -it 7f3ea bash -c "echo docker"
  docker
  ```
* Open a bash shell in the container and touch a file named hello-docker

  ```
  $ docker exec -it 7f3ea sh
  # touch hello-docker
  # ls
  bin  boot  dev  etc  hello-docker  home  lib  lib64  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
  # exit
  ```
* Stop the container and remove it. Write your comment about the file hello-docker

  ```
  $ docker rm -f 7f3ea
  7f3ea

  File is lost because containers are ephemeral
  ```


### Problem 3

* Run a container nginx with name nginx and attach a volume to the container

  ```
  $ docker run -d --name nginx -p 80:80 -v /usr/share/nginx/html:/usr/nginx-volume nginx
  bbd9fb8c72fe75db56a19fe3e5fb660e9bd4f834df5d284a1635d0ae20c51be7
  ```
* Remove the container & Run a new container with the following:


### Problem 4
