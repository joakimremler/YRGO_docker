# Docker

[<img src="https://media.giphy.com/media/6AFldi5xJQYIo/giphy.gif" alt="Docker" width="100%">](https://www.docker.com/)

> Docker is a tool designed to make it easier to create, deploy, and run applications by using containers. Containers allow a developer to package up an application with all of the parts it needs, such as libraries and other dependencies, and ship it all out as one package. By doing so, thanks to the container, the developer can rest assured that the application will run on any other Linux machine regardless of any customized settings that machine might have that could differ from the machine used for writing and testing the code. -- https://opensource.com/resources/what-docker

## Assignments

In this lession we are going to learn some basic skills about Docker. This includes how to install Docker and get the difference between an Docker Image and a Docker Container. We are also going to learn how to manage a Docker process and how to build and run a image.

## 1. Install docker on Droplet

The first thing you should do is to install Docker on your DigitalOcean Droplet. SSH to your server and follow [this](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04) guide.
You can start to do step 1 and 2.

## 2. Run a hello-world Container

To continue you can read step 3 and 4 from [DigitalOcean Docker Guide](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04). Where they explains the Docker concept about image and Containers. When you have read these steps you should now run your first container from a image called `hello-world`.

First you need to download the [hello-world](https://hub.docker.com/_/hello-world/) image from dockerhub by [pulling](https://docs.docker.com/engine/reference/commandline/pull/) it. Then you should [run](https://docs.docker.com/engine/reference/commandline/run/) this image.

You should now se a long message that contains a line with `Hello from Docker!`.

## 3. Run a ubuntu container inside ubuntu (?)

Keep reading [DigitalOcean Docker Guide](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04) step 5. When that is done you should go litte deeper into docker and run a ubuntu container inside our ubuntu server.

[<img src="https://media.giphy.com/media/l0IypeKl9NJhPFMrK/giphy.gif" alt="What!?" width="20%">](https://gph.is/2o1bMgY)

To do this find a [ubuntu](https://hub.docker.com/_/ubuntu/) image on Dockerhub. [Pull](https://docs.docker.com/engine/reference/commandline/pull/) this down and [run](https://docs.docker.com/engine/reference/commandline/run/) it with a `-it` [flag](https://docs.docker.com/engine/reference/run/#foreground).

You should now see a new bash terminal and this is from inside your running ubuntu container. If you look inside this container you will se that it is a totaly empty ubuntu installation. And if you install something inside this container and you restart the container it would be empty again.

You can exit the container with `exit` command.

But how can I install something insida a container that will constantly be there?

## 4. Create a Dockerfile

That is why we use [Dockerfiles](https://docs.docker.com/engine/reference/builder/#from). A Dockerfile is a instruction file that Docker uses to create a image with all of our new settings that we have added inside the Dockerfile and this is when it becomse really interesting.

Before we start to create a new Dockerfile you should [list](https://docs.docker.com/engine/reference/commandline/image_ls/) all images that is pulled to your server.

After that your new task should be to [build](https://docs.docker.com/engine/reference/commandline/build/) your own custom [image](https://docs.docker.com/engine/reference/commandline/image/) with a [Dockerfile](https://docs.docker.com/engine/reference/builder/#understand-how-arg-and-from-interact) and inside this image it should have a program called `htop`. By default the ubuntu image dosen't have this application.

Create a file with [nano](https://help.ubuntu.com/community/Nano) called `Dockerfile`

    $  nano Dockerfile

Add this content to the file:

      FROM ubuntu:16.04

      #Update image
      RUN apt-get update && apt-get install -y

      #Install htop
      RUN apt-get -y install htop

      #Set working directiv to container
      WORKDIR /app/yrgo

      #Run a bash loop and log output to logfile.log
      CMD exec /bin/sh -c 'trap : TERM INT; (x=1; while true; do echo "Welcome to container. Loop: $x"; echo "Welcome to container. Loop: $x" > logfile.log; sleep 5; x=$(( $x + 1 )); done) & wait'

Save the Dockerfile by pressing `Ctrl + x` then `y`.

Talk to the student next to you and discuss what you think this Dockerfile will do. If you have no idè, ask your teacher to explain.

## 5. Build a image

Then you should [build](https://docs.docker.com/engine/reference/commandline/build/#use-a-dockerignore-file) a new image from your Dockerfile with a `-t` flag, we will tag your new image `kalleanka/loop`.

> **Note** that it is a good practice to name new image to `yourname/scriptname` and when you run the build command don't forget the dot in the end.

After you have build your image you should [list](https://docs.docker.com/engine/reference/commandline/image_ls/) all Docker images, then you will see your new image listed.

## 5. Run your new image.

Now we have build our new image called `kalleanka/loop` we are ready to [run](https://docs.docker.com/engine/reference/run/#general-form) it. To run this container in the background we add a `-d` flag.

After that check that your new container is [running](https://docs.docker.com/engine/reference/commandline/ps/). If you can see a container that has IMAGE named `kalleanka/loop` you have successfully build and started your own Docker container.

## 6. Inspect container

Now when you have started a running container, you should be able to login into it and inspect it. To do this you have to get the `CONTAINER ID` of this container and you get it by [list](https://docs.docker.com/engine/reference/commandline/ps/) all docker processes.

    $ docker ps

And then get the `CONTAINER ID` and add it to:

    $ docker exec -it `CONTAINER ID` bash

You are now inside your container. You can see the output from the loop that is running inside your container with a cat command:

    $ cat logfile.log

And open `htop`, the application you installd inside the Dockerfile, by typing `htop`.

Exit htop by pressing `F10` and then exit container by typing `exit`.

## 7. Stop and delete running container

Before you are complete with this lession you should [stop](https://docs.docker.com/v17.09/engine/reference/commandline/stop/) your running container and then [remove](https://docs.docker.com/engine/reference/commandline/rm/) it.

To stop container:

    $ docker stop `CONTAINER ID`

To remove container:

    $ docker rm `CONTAINER ID`

If you now [list](https://docs.docker.com/engine/reference/commandline/ps/) all your Docker processes the output should now be empty.

## Complete!

[<img src="https://media.giphy.com/media/4Yn70mra350is/giphy.gif" alt="Complete!" width="50%">](https://gph.is/1Pwt4Xz)
