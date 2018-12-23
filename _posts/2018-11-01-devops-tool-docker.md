---
title:  "DevOps Tool : Docker"
search: true
categories: 
  - DevOps
  - Docker
last_modified_at: 2018-12-01T08:05:34-05:00
header:
  teaser: /assets/images/blog/devops-tool-docker/devops-tool-docker.png
---
![Docker](/assets/images/blog/devops-tool-docker/devops-tool-docker.png)

# Introduction

Docker is a tool used to perform operating system level virtualization (a.k.a containerization). The docker helps to run software through different containers. Many companies like Paypal, VISA and many more are using Docker to run their products.
I first encountered docker when I was exploring DevOps and the tools under DevOps. Docker got my attention and I started learning docker and guess what? I fell in love with it. The concept of containerization and how docker helped me to create containers very easily really fascinated me. 

# Why Docker

I just conveyed what docker is? and what is the purpose? Now we will discuss, why docker? The main issue that a Developer will face during his career is, the code not working in production server. But, it works just fine in their system. This issue is called environment issue. This issue is due to the difference in the configuration in the developer's PC and the server. Docker solves this issue by making a virtual environment with all the necessary dependencies. This step helps to solve the dependency issue. The other advantage of docker is the easy implementation of micro-services. Micro-services are the processes that communicate through a network. The communication is basically client-server communication (but done in small chunks). 

# Why implement Mirco-services?

The main advantage of implementing micro-services is the easy maintainability. Implementing micro-services helps to break the application into different chunks or pieces. These chunks or pieces are called services. These services are built in such a way that they have maximum cohesion and least coupling. Cohesion is the communication of different modules inside the service and coupling is the communication between 2 services. So, each service can be assigned to a different developer. As each developer assigns different dependencies ( depending on the application's need, personal preference and many more reasons), the docker file can incorporate these dependencies easily.
Before using Docker to implement micro-services, virtual machines where used. A virtual machine is an emulation of an actual PC. We can create virtual systems and install operating systems to run it. So to setup micro-services, the team had to create virtual machines (VM) and install operating systems and then run the service. That is, each service will be running on different virtual machines. Virtual machines can be made using applications like VirtualBox, VMware and many more. But, the best application for using virtual machines is KVM (Kernel Virtual Machine). But, KVM is only available to Linux. The main disadvantages of using VMs is that the developer has to specify the memory, processor count and disk space. The virtual machine will use these resource from the host machine even if the VM doesn't need it. The other disadvantage of using virtual machines is that it becomes impractical when working on a large scale implementation. On the other hand, using Docker helps in easy implement of micro-services. Each docker container can be easily programmed to be a service. Docker doesn't require any preallocation of memory, the container will automatically allocate the necessary resources dynamically.

# What is a Docker?

Docker is a simple tool that has been designed in such a way that it can create, deploy and run applications or services using containers. It is considered as a lightweight alternative to VMs. The docker requires a host machine to work and can allocate its RAM dynamically.

# Advantages of Docker

1. Rapid application development:  The docker containers require fewer runtime resources and require the least storage. Due to this form factor, they are very easy to deploy.
2. Portability: The services can be easily deployed in any servers via docker.
3. Version control: Just like Git, Docker container is version controlled. The developer can track the versions of Docker container (service). As Docker has version control, the developer can inspect changes in the file and can rollback changes.
4. Sharing: You can share your docker file with others through DockerHub. It is a remote repository to store docker files.
5. Secure: If the docker file fails, it won't affect the whole application. That is, a failed docker won't crash the server.

# How to use Docker work?

![Docker Working](/assets/images/blog/devops-tool-docker/docker-working.png)

A developer will develop a service and convert the service into a container using Docker. This process is done by creating a docker file, which in turn becomes an image. The developer will then add the dependencies for this service by creating or adding docker images to the file. Eg: For running a web-based application, the developer will add Nginx server docker image and PHP docker image. When the developer runs the docker file, these images work together to run the program. The docker image when run, generates a docker container. After the successful running of the docker container, the developer can push the docker image to DockerHub. He can then pull the docker image remotely from any computer and run the docker file there. If the developer had developed a docker file for the production server, he can easily pull the image from DockerHub and run the image in the server. 

# Docker Components

1. Docker Registry: Docker registry is the storage for all the docker images. These images can be public or private. The registry can be cloud-based or local. DockerHub is a cloud-based Docker registry. 
2. Docker image: A Docker image is a read-only template to create Docker containers. Docker image is built in such a way that it incorporates all the dependencies of the developed application.
3. Docker container: A docker container is a running instance of a Docker image. A container can be a combination of more than one docker image.

# Docker Bundle

The docker application consists of 4 software:-
1. Docker engine: Docker engine creates and runs Docker containers.
2. Docker CLI Client: Docker CLI client is the command-line interface to interact with Docker.
3. Docker Compose: Docker compose is used to define and run multi-container Docker applications.
4. Docker Machine: Docker machine is an application that lets the developer install docker engine on virtual hosts and helps the developer to manage the virtual hosts. 

# Docker Editions

There are two Docker editions:-
1. Docker CE (Community Edition): Docker CE is for the developers who have started learning docker.
2. Docker EE (Enterprise Edition): Docker EE is for enterprise level development.

# Docker Installation

## Mac

1. Download Docker for Mac using [this link](https://download.docker.com/mac/beta/Docker.dmg).
2. Install Docker from dmg.
3. After installation, open docker from applications.
4. After opening, the docker whale will be available in Mac's status bar. 
5. Open 'about Docker Desktop'  to know the docker engine's version and other relevant information.

![Docker Mac](/assets/images/blog/devops-tool-docker/about-docker-mac.png)

## Ubuntu / Debian

1. First, we will update the repositories.
```
$ sudo apt-get update
``` 
2. We will install the dependencies for Docker to work.
```
$ sudo apt install linux-image-extra-$(uname -r ) linux-image-extra-virtual -y
```
3. We will now install docker on the machine.
```
$ sudo apt-get install docker-engine
```
4. After installation, we have to start docker service.
```
$ sudo service docker start
```

## Fedora

1. Install dnf-plugins-core to manage Fedora's repositories.
```
$ sudo dnf -y install dnf-plugins-core
```
2. Add Docker repository to the machine.
```
$ sudo dnf config-manager \
    --add-repo \
    https://download.docker.com/linux/fedora/docker-ce.repo
```
3. Install Docker-CE
```
$ sudo dnf install docker-ce
```
4. Start docker service.
```
$ sudo systemctl enable docker
```
5. To start, stop, restart and get status about Docker, use the respective commands.
```
$ sudo systemctl start docker.service ## <-- Start docker ##
$ sudo systemctl stop docker.service ## <-- Stop docker ##
$ sudo systemctl restart docker.service ## <-- Restart docker ##
$ sudo systemctl status docker.service ## <-- Get status of docker ##
```

## RHEL / CentOS

1. Docker repo is already available in yum repository.
```
$ sudo yum install docker
```
2. Enable Docker service.
```
$ sudo systemctl enable docker.service
```
3. To start, stop, restart and get status about Docker, use the respective commands.
```
$ sudo systemctl start docker.service ## <-- Start docker ##
$ sudo systemctl stop docker.service ## <-- Stop docker ##
$ sudo systemctl restart docker.service ## <-- Restart docker ##
$ sudo systemctl status docker.service ## <-- Get status of docker ##
```


# Working with Docker

1. Pulling an image.
```
sudo docker pull docker-image
```
2. Run a Docker image.
```
sudo docker run docker-image
```
3. View Docker images.
```
sudo docker ps -as
```
or
```
sudo container ls
```
4. Remove Docker containers
```
sudo docker rm image-name
```
5. Remove Docker image
```
sudo docker image rm image-name
```