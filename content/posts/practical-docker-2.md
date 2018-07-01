+++ 
draft = false
date = 2018-06-26T18:22:59-07:00
title = "Dockerizing your project (Practical Docker: 2)"
slug = "" 
tags = []
categories = ["Docker"]
+++
---
### Overview of Practical Docker Series
This **Practical Docker** series is a step-by-step conceptual guide for people who is considering using Docker in their projects.

1. [Introduction to Docker (Practical Docker: 1)]({{< ref "posts/practical-docker-1.md" >}})
2. [Dockerizing your project (Practical Docker: 2)]({{< ref "posts/practical-docker-2.md" >}})
3. [Docker work flow in your team (Practical Docker: 3)]({{< ref "posts/practical-docker-3.md" >}})
4. [Advanced work flow for Docker (Practical Docker: 4)]({{< ref "posts/practical-docker-4.md" >}})

---
### What is covered in this post
In this second post of the **Practical Docker** series, we will go over how to create your Docker image and run it on your machine.

As a simple tutorial, we will create a lightweight Python web application which will be later loaded on your custom Docker image. 

### Install Docker
First, install [Docker Community Edition (CE)](https://docs.docker.com/install/) compatible to your operating system.

Once you are done installing, execute the Docker application which will run Docker daemon in the background which is responsible for managing your Docker containers.

### Test Docker installation
Docker provides a sample Docker image tagged as **library/hello-world**.

This Docker image contains a process which prints out *"Hello from Docker!"* and exits.

When you run **docker run hello-world**, following output should be printed.

```
docker run hello-world

Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
ca4f61b1923c: Pull complete
Digest: sha256:ca0eeb6fb05351dfc8759c20733c91def84cb8007aa89a5bf606bc8b315b9fc7
Status: Downloaded newer image for hello-world:latest

Hello from Docker!
This message shows that your installation appears to be working correctly.
...
```

Following things happend:

1. Docker daemon was not able to find an image named **hello-world**
2. **library/hello-world** image was found from Docker Hub which is a Docker image registry provided by Docker Inc.
3. Using the **library/hello-world** image, Docker daemon spun up a Docker container which prints out above messages.

### Docker CLI command cheat sheet
```
## List Docker CLI commands
docker
docker container --help

## Display Docker version and info
docker --version
docker version
docker info

## Execute Docker image
docker run hello-world

## List Docker images
docker image ls

## List Docker containers (running, all, all in quiet mode)
docker container ls
docker container ls --all
docker container ls -aq
```

### Let's Dockerize a Python application
First create a new directory to place a Dockerfile and a Python script

```
mkdir docker-test && cd docker-test
```

Create a Python script
```
touch webapp.py
```

Write following lines inside the **webapp.py** script
``` python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

if __name__ == "__main__":
    app.run(debug=True, host="0.0.0.0")
```

At this stage, you might ask *"Don't we need Python and Flask Python module to run the web application?"*

You are right in how we normally need to install dependencies on your local machine.

However, in this tutorial, we will try to **install all dependencies inside your custom Docker image**.

Create a Dockerfile
```
touch Dockerfile
```

Write following lines inside the **Dockerfile**
```docker
# your base image with Python3 pre-installed
FROM python:3

# current directory inside Docker image
WORKDIR /usr/src/app

# copy everything in your current local directory into current directory inside the Docker image
COPY . .

# install Python dependency
RUN pip install Flask

# command executed when Docker Container is created using this image
CMD python webapp.py
```

### Create your own Docker image

Build your Docker image named **my-first-docker-image**
```
docker build -t my-first-docker-image .
```

When you execute **docker image ls**, you should see an image named *my-first-docker-image*.

This image is a transportable image contains all Python dependencies and your web application.

Anyone who has an access to this image will now be able to run your web application without the need to install your web application specific dependencies on one's machine.

### Run a Docker container
Run a Docker Container using your Docker image
```
docker run -it -p 8000:5000 --rm --name my-first-docker-container my-first-docker-image
```

Above arguments seem intimidating, however it is like telling Docker daemon to 

1. run a Docker container using my-first-docker-image
2. name it my-first-docker-container
3. link your local machine's port 8000 to port 5000 of the Docker container where internal web application is listening

Open up your web browser and try accessing **localhost:8000** where you should see *Hello World!* on your screen.

### Review of what we did
1. There are tons of base images in [Docker Hub](https://hub.docker.com/explore/) with important dependencies pre-installed.
2. Choose a base image you would like to use
3. Write a Dockerfile which is an instruction set to build your custom Docker image
4. Build your Docker image
5. Run a Docker container using your built image

---
### Take home messages
1. Utilizing Docker allows clean deployment setup. 
2. By localizing all dependencies inside a Docker image, your application becomes very portable.
3. For example, your QA team is able to easily start a local testing environment with the newest build.
4. Automated deployment becomes more clean since all dependencies are localized within the Docker image.

In the next post of **Practical Docker** series, we will elaborate on usage of Docker within your development team.