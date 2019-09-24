# Docker

[<img src="https://media.giphy.com/media/6AFldi5xJQYIo/giphy.gif" alt="Docker" width="100%">](https://www.docker.com/)

> Docker is a tool designed to make it easier to create, deploy, and run applications by using containers. Containers allow a developer to package up an application with all of the parts it needs, such as libraries and other dependencies, and ship it all out as one package. By doing so, thanks to the container, the developer can rest assured that the application will run on any other Linux machine regardless of any customized settings that machine might have that could differ from the machine used for writing and testing the code. -- https://opensource.com/resources/what-docker

## Assignments

In this lession we are going to learn some basic skills about Docker. This includes how to install Docker and get the difference between an Docker Image and a Docker Container. We are also going to learn how to manage a Docker process and how to build and run a image.

## 1. Install docker on Droplet

The first thing you should do is to install Docker on your DigitalOcean Droplet. SSH to your server and follow [this](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04) guide.
You can start to do step 1 and 2.

Update server:

    $ sudo apt-get update && sudo apt-get upgrade

Use let apt-get use HTTPS:

    $ sudo apt install apt-transport-https ca-certificates curl software-properties-common

Add GPG key:

    $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

Add the Docker repository to APT sources:

    $ sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable"

Next, update the package database with the Docker packages from the newly added repo:

    $ sudo apt update

Make sure you are about to install from the Docker repo instead of the default Ubuntu repo:

    $ apt-cache policy docker-ce

Install Docker

    $ sudo apt install docker-ce

Check Status:

    $ sudo systemctl status docker

Add username to sudo group:

    $ sudo usermod -aG docker ${USER}

To apply the new group membership, log out of the server and back in, or type the following:

    $ su - ${USER}

Confirm that your user is now added to the docker group by typing:

    $ id -nG

## 2. Run a hello-world Container

To continue you can read step 3 and 4 from [DigitalOcean Docker Guide](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04). Where they explains the Docker concept about image and Containers. When you have read these steps you should now run your first container from a image called `hello-world`.

First you need to download the [hello-world](https://hub.docker.com/_/hello-world/) image from dockerhub by [pulling](https://docs.docker.com/engine/reference/commandline/pull/) it.

    $ docker pull hello-world

Then we should [run](https://docs.docker.com/engine/reference/commandline/run/) this image.

    $ docker run hello-world

You should now se a long message that contains a line with `Hello from Docker!`.

## 3. Run a ubuntu container inside ubuntu (?)

Keep reading [DigitalOcean Docker Guide](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04) step 5. When that is done you should go litte deeper into docker and run a ubuntu container inside our ubuntu server.

[<img src="https://media.giphy.com/media/l0IypeKl9NJhPFMrK/giphy.gif" alt="What!?" width="20%">](https://gph.is/2o1bMgY)

To do this find a [ubuntu](https://hub.docker.com/_/ubuntu/) image on dockerhub.

[Pull](https://docs.docker.com/engine/reference/commandline/pull/) this down and [run](https://docs.docker.com/engine/reference/commandline/run/) it with a `-it` [flag](https://docs.docker.com/engine/reference/run/#foreground).

Pull:

    $ docker pull ubuntu

Run it:

    $ docker run -it ubuntu

You should now see a new bash terminal and this is from inside your running ubuntu container. If you look inside this container you will se that it is a totaly empty ubuntu installation. And if you install something inside this container and you restart the container it would be empty again.

You can exit the container with `exit` command.

But how can I install something insida a container that will constantly be there?

## 4. Create a Dockerfile

That is why we use [Dockerfiles](https://docs.docker.com/engine/reference/builder/#from). A Dockerfile is a instruction file that Docker uses to create a image with all of our new settings that we have added inside the Dockerfile and this is when it becomse really interesting.

Before we start to create a new Dockerfile you should [list](https://docs.docker.com/engine/reference/commandline/image_ls/) all images that is pulled to your server.

You can do this by running:

    $ docker image ls

So your new task should be to [build](https://docs.docker.com/engine/reference/commandline/build/) your own custom [image](https://docs.docker.com/engine/reference/commandline/image/) with a [Dockerfile](https://docs.docker.com/engine/reference/builder/#understand-how-arg-and-from-interact) and inside this image it should have a program called `htop`. By default the ubuntu image dosen't have this application.

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

Then you should [build](https://docs.docker.com/engine/reference/commandline/build/#tag-an-image--t) a new image from your Dockerfile with a `-t` flag, we will tag your new image `kalleanka/loop`.

> **Note** that it is a good practice to name new image to `yourname/scriptname` and when you run the build command don't forget the dot in the end.

    $ docker build -t kalleanka/loop .

If you [list](https://docs.docker.com/engine/reference/commandline/image_ls/) all Docker images then you will see your new image.

    $ docker image ls

## 6. Run your new image.

Now we have build our new image called `kalleanka/loop` we are ready to [run](https://docs.docker.com/engine/reference/run/#general-form) it. To run this container in the background we add a `-d` flag.

    $ docker run -d kalleanka/loop

Check that your new container is [running](https://docs.docker.com/engine/reference/commandline/ps/).

    $ docker ps

If you can see a container that has IMAGE named `kalleanka/loop` you have successfully build and started a own Docker container.

## 7. Inspect container

Now when you have started a running container, you should be able to login into it and inspect it. To do this you have to get the `CONTAINER ID` of this container and you get it by [list](https://docs.docker.com/engine/reference/commandline/ps/) all docker processes.

    $ docker ps

And then get the `CONTAINER ID` and add it to:

    $ docker exec -it `CONTAINER ID` bash

You are now inside your container. You can see the output from the loop that is running inside your container with a cat command:

    $ cat logfile.log

And open `htop`, the application you installd inside the Dockerfile, by typing `htop`.

Exit htop by pressing `F10` and then exit container by typing `exit`.

## 8. Stop and delete running container

Before you are complete with this lession you should [stop](https://docs.docker.com/v17.09/engine/reference/commandline/stop/) your running container and then [remove](https://docs.docker.com/engine/reference/commandline/rm/) it.

To stop container:

    $ docker stop `CONTAINER ID`

To remove container:

    $ docker rm `CONTAINER ID`

If you now [list](https://docs.docker.com/engine/reference/commandline/ps/) all your Docker processes the output should now be empty.

## 9. Create a Volume

You should now create a new volume that you should share between two containers. The shared volume should be called `shared_volume`.

Create a volume:

    $ docker volume create --name shared_volume

List all volumes:

    $ docker volume ls

Delete volume:

    $ docker volume rm shared_volume

Inspect volume:

    $ docker volume inspect shared_volume

Hint: DigitalOcean has really good guides on Docker.

    https://www.digitalocean.com/community/tutorials/how-to-share-data-between-docker-containers

## 10. Share Volumes between containers

Run two containers one with [Ubuntu](https://hub.docker.com/_/ubuntu) and one with [Alpine](https://hub.docker.com/_/alpine). Connect Ubuntu and Alpine containers with the shared volume called `shared_volume`. You should now be able to create a file in the Ubuntu container and that file should now also be able in the Alpine container.

    $ docker run -ti --rm -v shared_volume:/public ubuntu
    $ cd public && echo 'hello' > 'hello.txt'

    $ docker run -ti --rm -v shared_volume:/public alpine
    $ ls /public

## EXTRA

## 11. Create and Share a Network between containers

Your final task is to create a shared network between multiply containers. When you are inside this containers you should be able to [ping](https://vitux.com/linux-ping-command/) the other containers.

    Create a new network:

    $ docker network create my_network

    Run Container A:

    $ docker run -it --rm --name container_a ubuntu

    Inside container_a run:

    $ apt-get update && apt-get install iputils-ping

    Run Container B:

    $ docker run -it --rm --name container_b ubuntu

    Inside container_b run:

    $ apt-get update && apt-get install iputils-ping


    Connect network to container_a:

    $ docker network connect my_network container_a

    Connect network to container_b:

    $ docker network connect my_network container_b


    Ping container_b inside container_a:

    $ ping container_b

    Ping container_a inside container_b:

    $ ping container_a

## Complete!

[<img src="https://media.giphy.com/media/4Yn70mra350is/giphy.gif" alt="Complete!" width="50%">](https://gph.is/1Pwt4Xz)
