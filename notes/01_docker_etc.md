# Notes: Session 1
## Linux/WSL set up

Can do an instruction PS1 = "> " in bash to remove all the in line nonsense in the terminal
then can do echo 'PS1 = "> "' > /.bashrc to make that happen in all terminals

## Docker (still not too sure what it is)
This needs to be configured for your WSL distro in the Docker desktop app settings. Once done you can run
the command:
docker
In the terminal to validate it works

A docker container completely isolates specific versions, packages etc from our host machine.
The idea is its an isolated container, unrelated to our system.

Can run to check configured correctly:
docker run hello-world

This is a "docker image", we can go inside a docker container by running: 

docker -it image_name

for example we might have: 

docker -it ubuntu

In this image, we are isolated from our host machine

We can then install packages, things inside our image. 

We can exit our container with ctrl+D

Every time we create a container from an image (i.e. docker run -it image_name) we create a new container
without anything in the container. 

The docker image defines the requirements for that container.

We can also use a different entrypoint:

docker run -it --entrypoint=bash python3.13.11-slim

this means we can run bash commands in our container.

We can view all docker containers using: docker ps -

Then we can use this to delete all containers: docker rm $(docker ps -a -q)

### Volumes in docker
A volume is available on both the host machine and the container as well.
To do this we can use the -v command. 

So below is an example we did: 

docker run -it --entrypoint=bash -v $(pwd)/test:/app/test python:3.13.11-slim

the -it tells us to make the new container and go into it
-- entrypoint=bash means we can use bash
-v tells us its a volume so is accessible by both machine and container
$(pwd)/test this is the location on our machine
/app/test this is the location in the container
python:3.13.11-slim this is the image part which contains image name and "type" (version)

This is sort of docker 101 around interacting with docker and volumes

## Data Pipelines
This is in general something that takes an input and gives an output. We, in this course, will work with the New York Taxi data setup. 

In here we will take a .csv file and put it in a psotrgres database.

