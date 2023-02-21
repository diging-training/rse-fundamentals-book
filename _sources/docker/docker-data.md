# Data and Docker

So far, we've talked about images and containers. We have seen how we can use containers to run software that wouldn't run on our host computer either because it doesn't run on our operating system or because we don't want to install all the required dependencies and the software itself. However, what we haven't talked is about the data that we might need to execute a program or the output a program might produce. 

Here is the thing though, a Docker container is separte from your host system. It is isolated from the rest of your system. This is good, because it gives you a certain amount of security (even if you run a container created by an evil hacker, the container won't be able to take over your system). However, this means that only data already present in the container is available for any program to use and data produced in the container are only available in the container. Once the container is shutdown and removed, so is the data. 


## Copying Data

To solve this issue, Docker provides the `docker cp` command. If you run this command, Docker will copy a file or folder from the host computer to the container or vice versa. 

Let's try it out. Open a terminal and run the `temperature-converter` container:

```
docker run -it --rm jdamerow/temperature-converter bash
```

Now, open another terminal and navigate to a folder you want to use for this exercise. Create a file:

```
echo "Hello World" > my-test-file.txt
```

Now copy this file into the running container:

```
> docker ps
CONTAINER ID   IMAGE                            COMMAND   CREATED         STATUS         PORTS     NAMES
35c544e884db   jdamerow/temperature-converter   "bash"    2 minutes ago   Up 2 minutes             hardcore_payne
docker cp my-test-file.txt hardcore_payne:/app
```

Go back to the terminal where you started the Docker container and check if the file has been copied into the `/app` folder.

```
> ls /app
convert.py  my-test-file.txt
```

Let's look at the copy command a little bit closer: 

```docker cp my-test-file.txt hardcore_payne:/app```

First we have the command (`docker cp`), then we tell Docker what file to copy (`my-test-file.txt`), and last we tell Docker where to copy the file to (into the container ` hardcore_payne` in the folder `/app`). 

```{note} When running the command on your computer, make sure to use the name of your Docker container (which will most likely not be <code>hardcore_payne</code>.)
```

If you want to copy a file from a container to your host system, you add the container name prefix (`hardcore_payne:`) to the first file (e.g. ```docker cp hardcore_payne:/app/my-test-file.txt my-second-test.txt```).

## Sharing Data with the Container

The above described solution works great if you only have to copy a file or directory once or twice. However, if you rerun your analysis multiple times or your container continuously generates data you need outside the container, using the `docker cp` command becomes cumbersome at best. Hence, Docker provides another solution: you can share folders between your host system and container. A shared folder is available in both your host system and your container. If you change a file in a shared folder, both systems have access to the file and its changes. The easiest way to achieve a shared folder is to *mount* a folder in your host system in a container:

```
docker run -it --mount type=bind,source=${PWD},target=/data jdamerow/temperature-converter bash
```

As you can see we are running the same command we used before but added `--mount type=bind,source=${PWD},target=/data`. This tells Docker to mount the folder at `${PWD}` (a variable that evalutes to our curren folder) to the folder `/data` inside the Docker container. Try it out! Once you are in the container, type `ls /data`. This should bring up a list of all the files in the folder you were currently in when starting the container. If you add a file in `/data` inside the container, that file will appear in your host system as well!