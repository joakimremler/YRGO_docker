# Docker

> Docker is a tool designed to make it easier to create, deploy, and run applications by using containers. Containers allow a developer to package up an application with all of the parts it needs, such as libraries and other dependencies, and ship it all out as one package. By doing so, thanks to the container, the developer can rest assured that the application will run on any other Linux machine regardless of any customized settings that machine might have that could differ from the machine used for writing and testing the code. -- https://opensource.com/resources/what-docker

## Assignments

## 1. Create a index file

Show slides with:
dockerhub
contianers
images

ps ls
run, build
port, volumes, ...

## L1

1. Install docker on server (Install Docker on Ubuntu)[https://docs.docker.com/install/linux/docker-ce/ubuntu/#install-docker-ce]
   $ sudo apt-get update
   $ sudo apt-get install docker-ce

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
