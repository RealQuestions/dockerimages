#Dockerfile for Titan container
#To run using bash:
#  docker run --name bashful_titan -it titan /bin/bash

FROM ubuntu:14.04

MAINTAINER christopher.andronikos@gmail.com

RUN apt-get update

RUN apt-get install -y software-properties-common
RUN add-apt-repository ppa:openjdk-r/ppa
RUN apt-get autoremove -y python3 software-properties-common

RUN apt-get update
RUN apt-get install -y openjdk-8-jre
RUN apt-get install -y openjdk-8-jdk
RUN apt-get -y upgrade

ADD titan /home/titan

#Will have to change if java version/implementation changes
RUN printf '\nJAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"' >> /etc/environment

WORKDIR /home/titan/titan-1.0.0-hadoop1
CMD bin/titan.sh start
