# Docker

We will start easy, let's run the test container Docker ships with.

## Hello World

```
docker pull hello-world
```

If you have never used this container before, you should  see some messages telling you that Docker is downloading the image for this container (*pulling* it).

Now, let's run a container from this image.

```
docker run hello-world
```

If everything goes as planned you should see this message:

```
Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (arm64v8)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
 ```

## Managing your Containers

Now, let's see all the containers we have. Type:

```
docker ps
```

You should see an empty table (unless you have any other containers running), something like this:

```
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

What happened to the hello-world container you might ask? `docker ps` prints only currently running containers, so unless your hello-world container is currently running, it won't be shown in the table. However, you can also list **all** containers (running or not). To do this, add the `-a` flag to the `ps` command.

```
docker ps -a
```

You should see something like this:

```
CONTAINER ID   IMAGE         COMMAND                  CREATED         STATUS                        PORTS     NAMES
cf2aec82cd77   hello-world   "/hello"                 6 seconds ago   Exited (0) 5 seconds ago                affectionate_ptolemy
```

The table tells you several things about your containers:
- Container id: The id of your container (`cf2aec82cd77`). You can use it to start/stop it, remove it, etc.
- Image: The image a container was created from (`hello-world` in this case.)
- Command: The command that is running in the container (the script `/hello`).
- Created: When the container was created.
- Status: The status of the container (e.g. if it is running or not). The container in the example exited 6 seconds ago.
- Ports: If the container exposes any ports, those would be listed here.
- Names: The name of the container. By default, Docker will generate names automatically (`affectionate_ptolemy`) but you can also specify names when creating containers.

Let's remove the hello-world container. We can do that using the `docker rm` command. Type `docker rm` and then add the name of your container. It will be different than the one here. Use `docker ps` to find out the name of your hello-world container. 

```
docker rm affectionate_ptolemy
```

If you run `docker ps -a` now, you should not see the hello-world container anymore.

If you know that you won't need a container anymore after it exits, you can tell docker to remove a container after it has been executed. Use the `--rm` parameter for that:

```
docker run --rm hello-world
```

If you run `docker ps -a` now, there should be no hello-world container.

## `run` vs. `start`

Docker provides two commands to start a container `run` and `start`. Those two commands are similar but have an important difference. 

`docker start` will start an **existing** container. The command requires you to specify the name or id of an existing container. If you try to run docker start with the name of an image, you will get an error message telling you that no such container exists.

```
> docker start hello-world
Error response from daemon: No such container: hello-world
```

`docker run` in contrast will first create a container from an image and then start the container. You need to provide the name of an image for the command to work, e.g. `docker run hello-world`.

## Docker images

Now that we know how to create and start containers, let's find out a little more about images. You can list all images on your computer with:

```
docker images
```

This will bring up a table similar to the one for containers.

```
REPOSITORY                       TAG       IMAGE ID       CREATED         SIZE
hello-world                      latest    46331d942d63   10 months ago   9.14kB
```

The table tells us for each image the name of the repository the image is provided from (`hello-world`), the tag of the image (`latest`), the id of the images, when it was created, and its size. Tags are labels that can be used to distinguish between different versions of an image. 


```{tip} <code>docker ps</code> is short-hand for <code>docker container ls</code>. Similarly, <code>docker images</code> is an alias for <code>docker image ls</code>. You can use both versions interchangably.
```

You can remove images with the command `docker rmi [image id]`, where `image id` is the id of the image you want to delete. Use `docker images` to find out the id of an image.

Once an image has been removed it will be relownloaded again if it is needed. For instance, you can remove the hello-world image. When you use `docker run hello-world` after that, the image will be pulled again.

```
> docker images
REPOSITORY                       TAG       IMAGE ID       CREATED         SIZE
hello-world                      latest    46331d942d63   10 months ago   9.14kB
> docker rmi 46331d942d63
Untagged: hello-world:latest
Untagged: hello-world@sha256:aa0cc8055b82dc2509bed2e19b275c8f463506616377219d9642221ab53cf9fe
Deleted: sha256:46331d942d6350436f64e614d75725f6de3bb5c63e266e236e04389820a234c4
Deleted: sha256:efb53921da3394806160641b72a2cbd34ca1a9a8345ac670a85a04ad3d0e3507
> docker run hello-world
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
7050e35b49f5: Pull complete 
Digest: sha256:aa0cc8055b82dc2509bed2e19b275c8f463506616377219d9642221ab53cf9fe
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (arm64v8)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
 ```

-> executing commands in docker container
-> docker run -it --rm jdamerow/temperature-converter
-> docker run -it --rm jdamerow/temperature-converter python ./convert.py 
-> docker run -it --rm jdamerow/temperature-converter