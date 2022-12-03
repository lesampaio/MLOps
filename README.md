# MLOps Pipeline
The main reference are the courses I take, but the content is enriched from other internet sources.

# Summary
- [Docker](#docker)
- [AWS](#aws)

## Docker
Principal reference -- Full Hands-On Course: [Docker Containers and Kubernetes Fundamentals by freeCodeCamp.org](https://www.youtube.com/watch?v=kTp5xUtcalw&list=PLk9o62WclVKHv2B6bgCg58DevqemyI51a&index=1&t=212s)

![Docker pipeline](/assets/docker-pipeline.jpg)

### What is a docker image?
A Docker image is a read-only template that contains a set of instructions for creating a container that can run on the Docker platform. It provides a convenient way to package up applications and preconfigured server environments, which you can use for your own private use or share publicly with other Docker users. 

Source: [Jfrog](https://jfrog.com/knowledge-base/a-beginners-guide-to-understanding-and-building-docker-images/)

### What is a docker container and docker image? Other definition
A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. A Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.

Source: [Docker - Container](https://www.docker.com/resources/what-container/)

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
Creates a copy of the data that is in the container to the machine, because if the container fails or is removed, the information will be saved regardless of the state of the container. Read more on [Alura: Creating volumes with docker](https://www.alura.com.br/artigos/criando-volumes-com-docker)

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

## Docker Compose
Compose is a tool for defining and running multi-container Docker applications. With Compose, you use a YAML file to configure your application's services. 

Source: [Compose documentation](https://docs.docker.com/compose/)

### Docker compose - Use cases
- Workloads that don't require full orchestrator
- Development and tests
- Use of a service that runs Docker Compose files
  - Azure app service
  - AWS ECS
  - Virtual machines

### Docker Compose Cheat Sheet
|Command|Definition|
|:--|:--|
|docker compose build |Build the images|
|docker compose start|Start the containers|
|docker compose stop|Stop the containers|
|docker compose up -d|Build and start|
|docker compose ps|List running containers|
|docker compose rm|Remove from memory|
|docker compose down -d|Stop and remove|
|docker compose logs|Display the logs from a container|
|docker compose exec [container] bash|Run a command line in container|

### Docker compose
**Build the service**

` docker compose build `

**Builds, (re)creates, starts, attaches to containers for a service**

` docker compose up `

**List the services**

` docker compose ls `

**Bring down what was created by UP**

` docker compose down `

# AWS
Reference -- Course: [AWS Expert - #ChamaAsMina by LINUXtips](https://www.linuxtips.io/)

## Core Concepts
- Master Account: 

        Parent container for all the accounts for the organization.
        Policy applied to the root is applied to all the organizational units (OUs) and accounts in the organization.
        There can be only one root currently and AWS Organization automatically creates it when an organization is created.

- Organizational Unit (OU): 

        A container for accounts within a root.
        An OU also can contain other OUs, enabling hierarchy creation that resembles an upside-down tree, with a root at the top and branches of OUs that reach down, ending in accounts that are the leaves of the tree.
        A policy attached to one of the nodes in the hierarchy, flows down and affects all branches (OUs) and leaves (accounts) beneath it.

- Accounts: 

        A standard AWS account that contains AWS resources.
        Each account can be directly in the root, or placed in one of the OUs in the hierarchy.
        Policy can be attached to an account to apply controls to only that one account.
        Accounts can be organized in a hierarchical, tree-like structure with a root at the top and organizational units nested under the root.

- Resources:

        In AWS, a resource is an entity that you can work with. Examples include an Amazon EC2 instance, an AWS CloudFormation stack, or an Amazon S3 bucket. If you work with multiple resources, you might find it useful to manage them as a group rather than move from one AWS service to another for each task.

- Service Control Policies: 

        A policy that specifies the services and actions that users and roles can use in the accounts that the SCP affects. SCPs are similar to IAM permissions policies except that they don't grant any permissions. 
        Instead, SCPs specify the maximum permissions for an organization, organizational unit (OU), or account. When you attach an SCP to your organization root or an OU, the SCP limits permissions for entities in member accounts. 

Reference: [Amazon AWS - Organizations](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_getting-started_concepts.html) | [Amazon AWS - Resource Groups](https://docs.aws.amazon.com/ARG/latest/userguide/resource-groups.html)

![AWS Organization](/assets/aws-organizations.png)

Source: [AWS Website](https://aws.amazon.com/pt/blogs/architecture/field-notes-how-factset-balances-developer-velocity-with-governance-using-aws-iam/)