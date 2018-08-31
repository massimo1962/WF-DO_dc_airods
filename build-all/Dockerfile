# Dockerizing MongoDB: Dockerfile for building MongoDB images
# Based on ubuntu:15.04, installs MongoDB following the instructions from:
# http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/
# Description:
# BASE MONGO
#
# imageName:'mongo_server:3.2'
# Use:
# build command: sudo docker build -t "mongo_server:3.6" .
# run command: sudo docker run -p 27017:27017 --name mongo_server -v /data/db2:/data/db -d [<docker_user>/]mongo_server:3.6


FROM       ubuntu:16.04
MAINTAINER massimo.fares@ingv.it


RUN apt-get update

# Installation:
# Import MongoDB public GPG key AND create a MongoDB list file
RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5

RUN echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.6 multiverse" | tee /etc/apt/sources.list.d/mongodb-org-3.6.list

# Update apt-get sources AND install MongoDB

RUN apt-get install -y apt-transport-https

RUN apt-get update


RUN apt-get install -y mongodb-org

# Create the MongoDB data directory
RUN mkdir -p /data/db

#install dependencies
RUN DEBIAN_FRONTEND=noninteractive apt-get install -y wget git vim python-dev python-pycurl python-simplejson \
    libcurl4-gnutls-dev libssl-dev pkg-config gcc-4.9 \
    python python-psutil python-requests python-jsonschema \
    python-setuptools python-dev build-essential python-pip \
    libxml2-dev libxslt1-dev libz-dev libfreetype6-dev \
    python-numpy python-scipy python-matplotlib

# mongo driver
RUN pip install pymongo

# irods driver
RUN pip install python-irodsclient

#make app dir
RUN mkdir -p /usr/src/collector

# obspy
WORKDIR /
RUN git clone https://github.com/obspy/obspy.git
WORKDIR /obspy

RUN pip install -e .


# Expose port #27017 from the container to the host
EXPOSE 27017

# Set /usr/bin/mongod as the dockerized entry-point application
ENTRYPOINT ["/usr/bin/mongod"]

