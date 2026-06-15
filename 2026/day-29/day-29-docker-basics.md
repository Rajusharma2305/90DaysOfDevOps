Day 29 – Docker Basics
Task 1: What is Docker?
What is a Container and Why Do We Need Them?

A container is a lightweight package that contains an application along with all its dependencies, libraries, and configuration files needed to run.

Why Containers?
Consistent environment across development, testing, and production.
Faster deployment.
Lightweight compared to virtual machines.
Easy application portability.
Efficient resource utilization.
Containers vs Virtual Machines
Feature	Containers	Virtual Machines
Virtualization	OS Level	Hardware Level
Boot Time	Seconds	Minutes
Resource Usage	Lightweight	Heavy
OS Required	Shares Host OS Kernel	Own Guest OS
Performance	Near Native	Slight Overhead
Size	MBs	GBs
Real Difference

Virtual Machines virtualize hardware and run complete operating systems.

Containers virtualize the operating system and share the host kernel, making them much faster and lighter.

Docker Architecture
Components
Docker Client

The command-line interface where users run Docker commands.

Examples:

docker run
docker build
docker pull
Docker Daemon (dockerd)
Runs in the background.
Builds images.
Creates containers.
Manages Docker objects.
Docker Images

Read-only templates used to create containers.

Example:

nginx:latest
ubuntu:24.04
Docker Containers

Running instances of Docker images.

Docker Registry

Stores Docker images.

Example:

Docker Hub
Private Registries
Docker Architecture Diagram
+----------------+
| Docker Client  |
| docker command |
+-------+--------+
        |
        v
+----------------+
| Docker Daemon  |
|   (dockerd)    |
+---+--------+---+
    |        |
    |        |
    v        v
Images   Containers
    ^
    |
    |
Docker Registry
(Docker Hub)

Flow:

User runs a Docker command.
Docker Client sends request to Docker Daemon.
Docker Daemon pulls image from Docker Hub if needed.
Docker Daemon creates and runs the container.
Task 2: Install Docker
Verify Installation
docker --version
docker info
Run Hello World
docker run hello-world

Expected Result:

Docker downloads the hello-world image.
Creates a container.
Runs the container.
Prints a success message.
Task 3: Run Real Containers
Run Nginx Container
docker run -d -p 8080:80 nginx

Check running containers:

docker ps

Open Browser:

http://localhost:8080

You should see the Nginx welcome page.

Run Ubuntu Container
docker run -it ubuntu bash

Try Linux commands:

pwd
ls
whoami
cat /etc/os-release

Exit:

exit
List Running Containers
docker ps
List All Containers
docker ps -a
Stop a Container
docker stop <container_id>

Example:

docker stop nginx
Remove a Container
docker rm <container_id>

Example:

docker rm nginx
Task 4: Explore Docker
Run in Detached Mode
docker run -d nginx
What is Different?
Container runs in background.
Terminal remains free for other commands.
Give a Custom Name
docker run -d --name my-nginx nginx

Check:

docker ps
Port Mapping
docker run -d -p 8080:80 nginx

Meaning:

Host Port = 8080
Container Port = 80

Access:

http://localhost:8080
View Logs
docker logs my-nginx

Follow logs continuously:

docker logs -f my-nginx
Execute Commands Inside Running Container
docker exec -it my-nginx bash

Or:

docker exec -it my-nginx sh

Example:

ls
pwd
hostname

Exit:

exit
