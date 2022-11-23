# MLOps Pipeline
The main reference are the courses I take, but the content is enriched from other internet sources.

# Summary
- [Docker](#docker)
- [AWS](#aws)

## Docker
Reference -- Full Hands-On Course: [Docker Containers and Kubernetes Fundamentals by freeCodeCamp.org](https://www.youtube.com/watch?v=kTp5xUtcalw&list=PLk9o62WclVKHv2B6bgCg58DevqemyI51a&index=1&t=212s)

Extra -- [Alura: Docker Volume](https://www.alura.com.br/artigos/criando-volumes-com-docker)

## Docker Extension VSCode
Docker extension in VSCode helps you with commands that run/build images and containers, creates necessary files (Dockerfile, .dockerignore, ...), etc. In addition, you can check the containers that are running, images, volumes, etc.

--------

### Docker CLI Cheat Sheet - Running and Stopping
|Command|Definition|
|:--|:--|
|docker pull [imageName]|Pull and image from a registry|
|docker run [imageName]|Run containers|
|docker run -d [imageName]|Detached mode|
|docker run start [containerName]|Start stopped containers|
|docker ps|List running containers|
|docker ps -a|List running and stopped containers (still in memory)|
|docker stop [containerName]|Stop containers but they will still be in memory|
|docker kill [containerName]|Kill containers that might be stuck in memory|
|docker image inspect|Get image info|
|docker images|List images|

- **imageName**: Name of the image that you find in the container registry
- **containerName**: Name of the running container

### Running a container
**Pull and run an nginx server**

` docker run --publish 8080:80 --name webserver nginx ` <br>
imageName -> nginx <br>
containerName -> webserver

**List the running containers**

` docker ps `

**Stop the container**

` docker stop webserver `

**Remove the container from memory**

` docker rm webserver `

**Remove the image**

` docker rmi nginx `

### Docker CLI Cheat Sheet - Building Containers
|Command|Definition|
|:--|:--|
|docker build -t [name:tag]|Builds an image using a Dockerfile located in the same folder|
|docker build -t [name:tag] -f [fileName]|Builds an image using a Dockerfile located in a different folder|
|docker tag [imageName] [name:tag]|Tag an existing image|

- **Dockerfile**: Text file that lists the steps to build an image
- **Docker tag**: Create a target image
    - **name:tag**: myimage:v1

### Building a container
**Build**

` docker build -t webserver:v1 `

**Run**

` docker run -d -p 8080:80 webserver:v1 `

**Display**

` curl localhost:8080 `

## Docker Volume
Creates a copy of the data that is in the container to the machine, because if the container fails or is removed, the information will be saved regardless of the state of the container. 

This is based on data persistence, read more about it at [DataStax](https://www.datastax.com/blog/what-persistence-and-why-does-it-matter).

### Volume Cheat Sheet
|Command|Definition|
|:--|:--|
|docker create volume [volumeName]|Creates a new volume|
|docker volume ls|List the volumes|
|docker volume inspect [volumeName]|Display volume info|
|docker volume rm [volumeName]|Deletes a volume|
|docker volume prune|Deletes all volumes not mounted|

### Mapping a volume
**Create a volume**

` docker volume create myvol `

**Inspect volume**

` docker volume inspect myvol `

**List the volumes**

` docker volume ls `

**Run a container with a volume**

` docker run -d --name devtest -v myvol:/app nginx:latest `
-  **myvol:/app**: Related folder inside container

# AWS
Reference -- Course: [AWS Expert - #ChamaAsMina by LINUXtips](https://www.linuxtips.io/)

## Core Concepts
- Master Account: 
- Organizational Unit (OU)
- Accounts (Sub accounts):
- Identity:
- Resources:

![AWS Organization](/assets/aws-organizations.png)

Source: [AWS Website](https://aws.amazon.com/pt/blogs/architecture/field-notes-how-factset-balances-developer-velocity-with-governance-using-aws-iam/)