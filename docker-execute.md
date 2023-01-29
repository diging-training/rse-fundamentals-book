# Running Commands in Docker Containers

In the last section, we learnt how to create Docker containers and run them. Running them meant that they executed predefined processes (e.g. printing a hello world message). There are many images that you can use that way, however, you can also choose what command a Docker container should execute. Try running the following:

```
docker run alpine echo "Hello World"
```

You should see something like this:

```
Unable to find image 'alpine:latest' locally
latest: Pulling from library/alpine
a9eaa45ef418: Pull complete 
Digest: sha256:f271e74b17ced29b915d351685fd4644785c6d1559dd1f2d4189a5e851ef753a
Status: Downloaded newer image for alpine:latest
Hello World
```

Docker first pulls the image from the registry (if you have not used it before), create a container and then print "Hello World", which is exactly what we told it to do!

What is happening? The alpine image is an image that provides a basic Alpine Linux system. It doesn't run any commands when you start a container created from the image but instead gives you access to the basic functionality of the operating system such as a shell. If you only run `docker run alpine` you won't get any output. However, when you run `docker run alpine [a command]` you tell the container to execute the given command in that operating system.

## Interacting with a running Container

This is cool! We can run commands in a Docker container that hasn't been predefined by the creator of the container. But it gets better! 

Run the following command:

```
docker run --rm jdamerow/temperature-converter python ./convert.py  
```

You should see the following error message:

```
Please, enter temperature in Celsius: Traceback (most recent call last):
  File "/app/./convert.py", line 1, in <module>
    celsius = float(input("Please, enter temperature in Celsius: "))
EOFError: EOF when reading a line
```

What is happening? The command pulls the image `jdamerow/temperature-converter`, creates and then runs a container from it. We tell the container to run the command `python ./convert.py`. This command, however, executes the `convert.py` script:

```
celsius = float(input("Please, enter temperature in Celsius: "))
fahrenheit = (celsius * 1.8) + 32 
print("{0} Celsius is {1} Fahrenheit.".format(celsius, fahrenheit)) 
```

All this script is doing is asking for input from the user (a number representing degree in Celsius), calculating the degree in Fahrenheit from it, and then printing the result. However, the container does not let us provide an input, so the script errors out (with the error message seen above).

Try adding `-i` to the command:

```
docker run -i --rm jdamerow/temperature-converter python ./convert.py  
```

You should now be able to enter a number! The `-i` flag stands for `interactive` and allows you to interact with the container. This now let's you basically run any software you can run through the terminal even if you don't have the necessary dependencies on your computer. For instance, to run the above Python script, you do not need Python installed! 

And it gets even better! Try adding the `-t` flag to the command and remove the Python script command like this:

```
docker run -it --rm jdamerow/temperature-converter
```

You should get the following output:

```
Python 3.9.16 (main, Jan 23 2023, 23:47:45) 
[GCC 10.2.1 20210110] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```
This is the Python interpreter! You can now use it the same way (almost) as you would use on your host system. Type `exit()` to exit out of it.

The `-t` flag stands for `tty`. In simple terms, this means that you get a terminal connection to the container. The terminal connection lets you interact with the Python interpreter. If you execute `docker run -it --rm jdamerow/temperature-converter bash` it gives you access to a bash shell inside the container.

-> executing commands in docker container
-> docker run -it --rm jdamerow/temperature-converter
-> docker run -it --rm jdamerow/temperature-converter python ./convert.py 
-> docker run -it --rm jdamerow/temperature-converter

