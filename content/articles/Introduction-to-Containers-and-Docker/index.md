---
layout: engineering-education
status: publish
published: true
url: /Introduction-to-Containers-and-Docker/
title: Introduction to Containers and Docker
description: In this article, you will learn about containers, containerization, docker or docker-engine, docker client-server architecture, and why Docker is so popular in the software business industry.
author: evans-chaun
date: 2021-07-20T00:00:00-21:00
topics: [Containers]
excerpt_separator: <!--more-->
images:

  - url: /engineering-education/Introduction-to-Containers-and-Docker/hero.png
    alt: Introduction to Containers and Docker example image
---  

To grasp what `Docker` is and why it is employed, you must first realize what `containers` are and what problems they solve. Containers are entirely isolated environments constructed on top of an existing operating system to create a `virtual barrier` between the app running inside and the outside world. Docker, on the other hand, is a piece of software that allows us to manage the lifetime of these containers.

### Prerequisites

To follow along with this article smoothly, you need to have:

- A computer running any operating system.
- Some knowledge of apps that run from the command-line interface.

### Table of contents
 
- [Container terminologies](#container-terminologies)

- [Introduction to docker](#introduction-to-docker) 
 
- [Reasons why we use dockers](#reasons-why-we-use-dockers)

- [Docker Desktop for Windows requirements and installation](docker-desktop-for-windows-requirements-and-installation) 

- [Conclusion](#conclusion) 

### Container terminologies

1. **Container**: A container is a separate operating system environment in which one or more programs can run, generally with only the resources required for the application to perform properly. 
2. **Container image**: A container image is a self-contained piece of software that contains all of the code, tools, and resources needed to execute.
3. **Docker file**: It is a book record that contains directions for building a Docker image.
4. **Docker Hub**: It is a cloud-based registry that lets you download images from other communities from Docker.
5. **Repository**: A Docker repository is a collection of Docker images that all have the same name but differ in tags or versions.
6. **Registry**: It is a Docker image repository. Docker clients connect to registries to download or upload images they've produced using the pull and push commands. There are both public and private registers.
7. **Docker Engine**: Docker Engine, is a software component that lets you manage the container's life cycle, describes how to set up it, and software and services you use within it. It also describes how you can quickly destroy and restart your containers.
8. **Docker Compose**: It is a program that allows you to create and execute multi-container Docker applications. You set up your application's services using Compose which uses a YAML file. You then build and start all of the services from your setup with a single command.
9. **Orchestration and cluster management**: Orchestration is a system monitoring and management tool. In huge compartment arrangements, tooling is crucial for screen and oversee pictures, containers, and hosts through a Command-line interface (CLI) or a Graphical user interface(GUI). 
10. **Volumes**: For storing data created by and utilized by Docker containers, volumes are the ideal method. Unlike bind mounts, which are dependent on the directory structure and operating system of the host computer, Docker manages volumes entirely.

### Introduction to docker

`Docker`, also known as `Docker Engine`, is a piece of software that allows us to manage the lifecycle of containers, describing how they will be set up, what applications/software/services will run within them, their networking and storage requirements, and, if necessary, how to quickly destroy and restart them.

Docker runs processes within containers using `Docker images`. A Docker image is a file that is used by a Docker container to run programs. Docker images, like a template, serve as a collection of instructions for constructing a Docker container. When utilizing Docker, Docker images also serve as a starting point. In `Virtual Machine` (VM) settings, an image is similar to a snapshot.

> Because containerization is a Linux OS feature, docker can only be installed on Linux operating systems such as Ubuntu, Fedora, Redhat, and so on. You'll need to construct a Linux virtual machine if you want to utilize Docker on a Windows operating system. The Docker Windows application creates a virtual machine automatically and executes the Docker engine. 

For a client-server architecture, Docker is made up of three elements: 

1. Process of a server daemon (docker). The docker daemon creates and manages docker objects, such as containers, pictures, networks, and volumes.

2. An API to communicate from applications with the Docker daemon. The API connects to the Docker daemon process via the command-line interface. 

3. A Docker command-line interface (CLI) for running Docker commands that allows us to perform various tasks on the docker daemon process.

### Reasons why we use dockers

Recently, Docker has grown highly popular in the software industry. It lets developers and system admins construct and operate applications in containers, thanks to the growing need for microservices and DevOps. Certain elements contributing to the popularity of Docker are: 

1. **Multifunctionality**: A docker container allows you to run any heavy-weight application, or even an operating system, using a simple hello world application, a web server like Apache HTTP Server, and Nginx. Although Docker does not advise running an operating system within a container, it is still possible to do so.

2. **Containers in Docker are freely linked.**: A container is a self-contained entity with its resource quota, networking configuration, and other features that make it easier for system administrators to replace or update one container without impacting the others.

3. **Highly secure**: Docker's Highly Secure feature ensures that containers are entirely isolated from outside processes.

4. **Docker containers are small and portable**: Docker containers are lighter than virtual machines since they establish separate user spaces and use the underlying OS Kernel of the system on which they are run.

5. **It is portable**: When we finish building an application on our local workstation and need to deploy it to production, we usually run into several problems with environment configuration. However, if you use Docker, you can describe the container setup procedures, and Docker will ensure that the environment is set up the same way every time you run it.

### Docker Desktop for Windows requirements and installation

Docker is an OS-level virtualization programming stage that assists clients with building and overseeing applications in the Docker environment with all its library conditions. Before we examine Dockers Installation on Windows, let us first understand the requirements needed to introduce Docker for Windows. 

#### Docker Desktop for Windows system requirements:

For Dockers installation to run as planned, your PC ought to meet the following requirements: 

1. A Windows 10 64-bit OS. Also, the `Virtualization and Containers` Windows feature should be enabled.

2. A minimum of 4GB system RAM is recommended. 

> When Hyper-V is activated on Windows, any designed VirtualBox on your framework will quit working. 

#### Docker Installation on Windows Step-By-Step. 

1. Download the Docker Desktop for Windows executable record. To download the official file, [click here](https://docs.docker.com/docker-for-windows/install).

2. Double click on the `Docker Desktop Installer.exe` to start the installation. You might be prompted to enable the Hyper-V and Windows Containers feature after the installation has started. Please ensure that you do so.

3. Accept the Terms and Agreement to allow the installation cycle to finish.

4. After the installation, you can open the Docker Desktop program by clicking Finish.

You have successfully launched a Docker Desktop application!

### Conclusion

In this article, we learned about containers, containerization, docker or docker-engine, docker client-server architecture, and why Docker is so popular in the software business industry. I urge the reader to dig deeper into docker to be better skilled in software development.

### Further reading

1. [Introduction to Containers and Docker](https://docs.microsoft.com/en-us/dotnet/architecture/microservices/container-docker-introduction/)
2. [A Beginner-Friendly Introduction to Containers, VMs and Docker](https://www.freecodecamp.org/news/a-beginner-friendly-introduction-to-containers-vms-and-docker-79a9e3e119b/)
3. [Introduction to Docker and Containers](https://www.oreilly.com/attend/introduction-to-docker-and-containers/0636920359579/0636920056161/)

---

Peer Review Contributions by: [Willies Ogola](/engineering-education/authors/willies-ogola/)
