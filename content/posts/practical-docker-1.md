+++ 
draft = false
date = 2018-06-26T17:59:21-07:00
title = "Introduction to Docker (Practical Docker: 1)"
slug = "" 
tags = []
categories = ["Docker"]
+++
---
### Overview of Practical Docker Series
This **Practical Docker** series is a step-by-step conceptual guide for people who is considering using Docker in their projects.

Starting from this introductory post, I will be writing following posts leading to practical usage of Docker in real life. 

1. [Introduction to Docker (Practical Docker: 1)]({{< ref "posts/practical-docker-1.md" >}})
2. [Dockerizing your project (Practical Docker: 2)]({{< ref "posts/practical-docker-2.md" >}})
3. [Docker work flow in your team (Practical Docker: 3)]({{< ref "posts/practical-docker-3.md" >}})
4. [Advanced work flow for Docker (Practical Docker: 4)]({{< ref "posts/practical-docker-4.md" >}})

---
### What is Docker
[Docker](https://www.docker.com/) is a container technology.

It is called a **container technology** since it allows **encapsulating and isolating** your application with its dependencies.

### Container Technology VS Virtual Machine
People are more familiar with **Virtual Machine** technology which creates another OS layer on top of ones original OS.

{{< figure src="images/practical-docker/vm-vs-container.jpg" caption="source (https://rancher.com/playing-catch-docker-containers/)" >}}

As seen from the above figure, container technology does not require additional OS to be installed. 

This **encapsulated and isolated** process shares your kernel along with other processes on your machine. This encapsulated process uses different kernel namespace which ensures security while eliminating the overhead of installing another OS.  

### Similarities
When installing a VM, you first download an image file with **.iso** extention usually.

In Docker, a **Dockerized image** is what you use to get your Docker process up and running.

### Differences
VM file system is persistent, which means modifications to the VM file system stays the same after a reboot.

In Docker, any time you run a process based on a Dockerized image, brand new process is created. However, there is a way to use persistent storage by mounting a volume to it.

Following analogy can be useful in understanding the terminology difference between Docker image and Docker container.

1. **Java Compiled Code : Java Process = Docker Image : Docker Container**
2. **OOP Class : OOP Instance = Docker Image : Docker Container**

As you see, from a Docker image, you can spin up multiple Docker containers as if you are running multiple Java processes based on a single compiled code.

### Why use Docker
1. Docker has much much less overhead in size and has better performance compared to VM technologies.
2. All dependencies are encapsulated within a Docker image. This allows your development and production machine to maintain clean environments.
3. If it works on your development machine, it will work on any other machines not limited to operating systems. This includes your deployment machine as well.

### Summary
Docker is:

1. Container technology
2. Shares linux kernel
3. Less overheads than virtual machine
4. Cross-platform
5. Promotes single-responsibility principle. Single process per container

In the next post of **Practical Docker** series, we will go over how to create a Docker image and run a Docker container.
