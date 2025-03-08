# docker command notes

## first, launch docker desktop

## check docker version
> docker version

---

## images

### pull image
```docker pull <image_name>```
> docker image pull ubuntu:20.04

### list image
> docker image ls | grep "ubuntu"
> docker image ls -a
> docker images

### inspect image
> docker image inspect ubuntu:20.04
### check image history
> docker image history ubuntu:20.04

### tag image (rename image)
```docker image tag <image_name> <new_image_name>```
> docker tag 8e5c4f0285ec ubuntu:20.04

### remove/delete image
```docker image rm <image_name>```
> docker image rm ubuntu:20.04
```docker rmi <image_id>```
> docker rmi 8e5c4f0285ec

### (dangerous) remove all images
```docker image prune```
> docker image prune

---

## containers

### run container

- A basic way to _start_ a docker container is:
  ```> docker run --name my-container -d repository-name```

- The above command starts a container based on the image `repository-name`. If
  the specific image is _not_ present on your machine, docker automatically
  `pulls` the image from DockerHub

- The parameters:
  - `--name`: Allows you to specify a name for your container; if you don't add
    this parameter, docker randomly generates a name for you
  - `-d`: Runs the container in the background (stands for "detached")

- Once you start a container in the background, it will keep running until you
  `stop` it like so:

#### Start a simple container and run a bash shell inside
> docker run -it ubuntu:20.04 /bin/bash
```docker container run -it <image_name>:<tag> /bin/bash --name <container_name>```
> docker container run -it ubuntu:20.04 /bin/bash --name percy
##### Log in from a different window - Accessing Containers
> docker container exec -it percy bash
  - `-it`: Instructs Docker to allocate a pseudo-TTY connected to the container’s
    `stdin` (standard input); creating an interactive bash shell in the container.
##### get outside of the running container
> exit

### list all containers
> docker container ls -a
> docker ps -a
> docker ps -a | grep "percy"
#### List running containers only
> docker ps
#### List only stopped containers
> docker ps -a -f status=exited

### stop container
```docker stop <container_id>```
> docker container stop percy

### restart container
> docker restart percy

### remove/delete container
```docker rm <container_id>```
> docker rm percy
> docker container rm percy
> docker container rm -f percy
#### Remove all stopped containers
> docker container prune

### Copying Files into Containers

Since containers have their own independent environment and file system, they
can only see the files within that file system. In some situations you will want
to write code in your host machine\'s environment and then run that piece of
code within the container. To copy files into the container you can:

```
> docker cp file container-name:/path/where/to/copy/file
```

---


### Docker Help

- To find out more about the different docker commands:
  ```
  > docker COMMAND --help
  ```


---


