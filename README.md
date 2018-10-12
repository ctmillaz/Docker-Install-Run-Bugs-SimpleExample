# Docker-Install-Run-Bugs-SimpleExample


### Update CentOS
`sudo yum update`

### Add Docker Repo
`curl -fsSL https://get.docker.com/ | sh`

### Install docker
`yum install docker`

### You must be root to run docker
`su`

### Start docker service
`systemctl start docker`

### Run a docker container
`docker run <image name>`

### Check to see images available
`docker images`

### Check to see processes running
`docker ps`

### How to stop a docker container
`docker kill <container name> OR docker stop <container name>`

### How to build docker file
### -t flag to tag the image as what ever tag name you would like, and look in the current directory for the dockerfile
`docker build -t <tag_name> .`
------------------------------------------------------------------------------------------------------------------------


##Dockerfile Example

`
FROM centos



RUN yum install -y java



VOLUME /tmp

ADD /spring-boo-web-0.0.1-SNAPSHOT.jar myapp.jar 

RUN sh -c 'touch /myapp.jar'

ENTRYPOINT ["java", "-Djava.security.egd=file:/dev/./urandom","-jar", "/myapp.jar"]
`

------------------------------------------------------------------------------------------------------------------------


## Problem:
### Resolve issue: Job for docker.service failed because the control process exited with error code. 
### See "systemctl status docker.service" and "journalctl -xe" for details.

## Solution:
`sudo rm -rf /var/lib/docker`
`sudo systemctl docker start`


## Problem
### WARNING: IPv4 forwarding is disabled. Networking will not work.

## Solution:
`nano /etc/sysctl.conf`
### change net.ipv4.ip_forward=0 to be 
`net.ipv4.ip_forward=1`
`systemctl restart network`
`sysctl net.ipv4.ip_forward`
`docker run -d <image name>`
