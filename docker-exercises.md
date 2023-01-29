# Docker Exercises

1. Create and run a container of the `hello-world` image. What is printed on the console after you do that? Did Docker pull the image from the repository or was it already present on your system?

1. Print all Docker images on your computer. How many are there? Then print all containers. How many are there? Do you have at least one container for each image? Do you have more than one container per image? If so, why?

1. Run the command `cat /etc/os-release` in an alpine container. What does it print?

2. Run the following command `docker run -it --rm jdamerow/temperature-converter bash`. Then get a list of all the files in the `/app` folder in the container. Then run `python convert.py`.

Take a screenshot of the output of each of the commands.