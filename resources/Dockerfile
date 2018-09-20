FROM ubuntu:16.04

#Update image
RUN apt-get update && apt-get install -y

#Install htop
RUN apt-get -y install htop

#Set working directiv to container
WORKDIR /app/yrgo

#Run a bash loop and log output to logfile.log
CMD exec /bin/sh -c 'trap : TERM INT; (x=1; while true; do echo "Welcome to container. Loop: $x"; echo "Welcome to container. Loop: $x" > logfile.log; sleep 5; x=$(( $x + 1 )); done) & wait'