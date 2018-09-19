# Docker

> Docker is a tool designed to make it easier to create, deploy, and run applications by using containers. Containers allow a developer to package up an application with all of the parts it needs, such as libraries and other dependencies, and ship it all out as one package. By doing so, thanks to the container, the developer can rest assured that the application will run on any other Linux machine regardless of any customized settings that machine might have that could differ from the machine used for writing and testing the code. -- https://opensource.com/resources/what-docker

## Assignments

## 1. Install docker on Droplet

The first thing you should do is to install Docker on your DigitalOcean Droplet. SSH to your server and follow [this](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04) guide.
You can start to do step 1 and 2.

S:
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

To continue you can read step 3 and 4 from [DigitalOcean Docker Guide](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04). Where they explains the Docker concept about image and Containers.

You should now run your first container from and simple image called [hello-world](https://hub.docker.com/_/hello-world/).

But first we download the new image from dockerhub by [pulling](https://docs.docker.com/engine/reference/commandline/pull/) it. Write this command in the terminal in the server:

    $ docker pull hello-world

Then we should [run](https://docs.docker.com/engine/reference/commandline/run/) this image:

    $ docker run hello-world

You should now se a long message that contains `Hello from Docker!`.

## 3. Run a ubuntu contianer inside ubuntu (?)

Keep reading [DigitalOcean Docker Guide](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04) step 5.

With that done we should go litte deeper into docker and run a ubuntu container inside our ubuntu server.
[<img src="https://media.giphy.com/media/l0IypeKl9NJhPFMrK/giphy.gif" alt="What!?" width="20%">](https://gph.is/2o1bMgY)

To do this find a ubuntu image on dockerhub. [Hint!](https://hub.docker.com/_/ubuntu/).
[Pull](https://docs.docker.com/engine/reference/commandline/pull/) this down and [run](https://docs.docker.com/engine/reference/commandline/run/) it with a `-it` flag.

s:
$ docker run -it ubuntu

## 4. Build a image with a Dockerfile

node image witha a app.js node server file

Show slides with:
dockerhub
contianers
images

ps ls
run, build
port, volumes, ...

2. Run (hello world)[docker run hello-world]
   $ docker run hello-world

3. Run Ubuntu inside ubuntu [https://media.giphy.com/media/l0IypeKl9NJhPFMrK/giphy.gif](https://media.giphy.com/media/l0IypeKl9NJhPFMrK/giphy.gif)
   $ docker run -it ubuntu bash

4. Run a simple node web application from dockerhub joakimremler

5. Create a dockerfile with a simple node application with support of mysql

## L2 Grupp arbete?

6. Docker stack Node + mysql + react
   > Se hur allt hänger ihop

https://media.giphy.com/media/jYjA6fHBfAZvq/giphy.gif
