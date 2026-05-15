# DOCKER NOTES

Docker is a containerization platform.
It helps package application + dependencies + runtime + libraries together.

Main idea:
"Build once, run anywhere"

Earlier problem:
Works in local machine but fails in server.

Reasons:

- Different Python versions
- Missing dependencies
- OS mismatch
- Manual setup issues

Docker solves this by creating isolated containers.

# Virtual Machine vs Docker

## Virtual Machine

- Heavy
- Has full guest OS
- Uses more RAM
- Slow startup

Architecture:
Hardware
Host OS
Hypervisor
Guest OS
Application

## Docker Container

- Lightweight
- Shares host kernel
- Fast startup
- Less memory

Architecture:
Hardware
Host OS
Docker Engine
Containers

Main understanding:
Docker containers are not full operating systems.

---

# Important Docker Components

## Docker Engine

Main service running Docker.

## Docker Image

Blueprint/template.

Example:
ubuntu image
nginx image
python image

Image is read-only.

## Docker Container

Running instance of image.

One image can create multiple containers.

Example:
1 nginx image
5 nginx containers

## Docker Hub

Public registry to download images.

Like GitHub but for Docker images.

---

# Installing Docker (Ubuntu)

Update packages:

```bash
sudo apt update
```

Install Docker:

```bash
sudo apt install docker.io -y
```

Check version:

```bash
docker --version
```

Check service:

```bash
systemctl status docker
```

Start docker:

```bash
sudo systemctl start docker
```

Enable at boot:

```bash
sudo systemctl enable docker
```

---

# Exercise

Pulled ubuntu image:

```bash
docker pull ubuntu
```

Internally:

1. Docker checked local machine
2. Image not found
3. Downloaded from Docker Hub
4. Stored locally

Checked images:

```bash
docker images
```

Output showed:

- repository
- tag
- image id
- size

---

# First Container

```bash
docker run ubuntu
```

Container started and exited immediately.

Reason:
Ubuntu image had no foreground process running.

Then I tried interactive mode:

```bash
docker run -it ubuntu
```

Now I got shell access inside container.

Commands I tested:

```bash
ls
pwd
whoami
```

Exited using:

```bash
exit
```

---

# Understanding -it

-i => interactive
-t => terminal

Together:

```bash
docker run -it ubuntu
```

Provides terminal inside container.

---

# Listing Containers

Running containers:

```bash
docker ps
```

All containers:

```bash
docker ps -a
```

Observed:
Exited containers are also stored.

---

# Container Lifecycle

create -> run -> stop -> remove

Stop container:

```bash
docker stop <container_id>
```

Start again:

```bash
docker start <container_id>
```

Attach:

```bash
docker attach <container_id>
```

Remove:

```bash
docker rm <container_id>
```

---

# Running Nginx Container

```bash
docker run nginx
```

Again container started.

But browser was not accessible.

Reason:
Port not exposed.

---

# Understanding Port Mapping

Command:

```bash
docker run -p 8080:80 nginx
```

Meaning:
8080 => local machine port
80 => container port

Access:

```text
http://localhost:8080
```

This was my first successful browser test.

---

# Detached Mode

Running container in background:

```bash
docker run -d nginx
```

-d => detached mode

Useful for servers.

---

# Naming Containers

Instead of random names:

```bash
docker run --name mynginx nginx
```

Very useful while stopping/removing containers.

---

# Executing Commands Inside Running Container

```bash
docker exec -it mynginx bash
```

This opens shell inside already running container.

Commands I tested:

```bash
apt update
cd /usr/share/nginx/html
```

---

# Logs

View logs:

```bash
docker logs <container_id>
```

Follow logs:

```bash
docker logs -f <container_id>
```

Useful for debugging.

---

# Dockerfile

Dockerfile is used to create custom images.

Basic structure:

```dockerfile
FROM python:3.11

WORKDIR /app

COPY . .

RUN pip install -r requirements.txt

CMD ["python", "app.py"]
```

---

# Understanding Dockerfile Instructions

## FROM

Base image.

Example:

```dockerfile
FROM ubuntu
```

## WORKDIR

Sets working directory.

## COPY

Copies files from local machine.

## RUN

Executes during image build.

## CMD

Runs when container starts.

---

# Flask App Dockerization

Project structure:

```text
app.py
requirements.txt
Dockerfile
```

app.py:

```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def home():
    return "Docker Working"

app.run(host="0.0.0.0", port=5000)
```

requirements.txt:

```text
flask
```

Dockerfile:

```dockerfile
FROM python:3.11

WORKDIR /app

COPY . .

RUN pip install -r requirements.txt

CMD ["python", "app.py"]
```

---

# Building Custom Image

```bash
docker build -t flaskapp .
```

What happened:

1. Docker read Dockerfile
2. Pulled base image
3. Copied files
4. Installed dependencies
5. Created image

Checked:

```bash
docker images
```

---

# Running Custom Image

```bash
docker run -p 5000:5000 flaskapp
```

Application opened successfully in browser.

---

# Docker Volumes

Problem:
Container data gets deleted after container removal.

Solution:
Volumes.

Create volume:

```bash
docker volume create myvolume
```

Use volume:

```bash
docker run -v myvolume:/data ubuntu
```

Important understanding:
Volume data persists even if container is deleted.

---

# Bind Mounts

Mount local folder:

```bash
docker run -v $(pwd):/app ubuntu
```

Useful during development.

Changes in local files reflect inside container.

---

# Docker Networks

Containers communicate using networks.

Create network:

```bash
docker network create mynetwork
```

Run containers:

```bash
docker run --network=mynetwork nginx
```

---

# Docker Compose

Used for multi-container applications.

Example:

- frontend
- backend
- database

docker-compose.yml:

```yaml
version: "3"

services:
  web:
    image: nginx
    ports:
      - "8080:80"

  db:
    image: mysql
```

Run:

```bash
docker compose up
```

Background:

```bash
docker compose up -d
```

Stop:

```bash
docker compose down
```

---

# Docker Registry

Push image to Docker Hub.

Login:

```bash
docker login
```

Tag image:

```bash
docker tag flaskapp username/flaskapp
```

Push:

```bash
docker push username/flaskapp
```

---

# Common Errors I Faced

1. Permission denied
   Solution:

```bash
sudo usermod -aG docker $USER
```

2. Port already allocated
   Reason:
   Port already used by another container.

3. Container exits immediately
   Reason:
   No foreground process.

---

# Docker Cleanup Commands

Remove stopped containers:

```bash
docker container prune
```

Remove unused images:

```bash
docker image prune
```

Remove everything unused:

```bash
docker system prune
```

---

# Summary

Things I understood:

- Docker creates isolated environments
- Containers are lightweight
- Images are templates
- Dockerfile automates builds
- Docker Compose manages multiple services

Things I should practice more:

- Networking
- Compose
- Multi-stage builds
- Docker security

---

# Commands Cheat Sheet

```bash
docker --version
docker pull ubuntu
docker images
docker ps
docker ps -a
docker run -it ubuntu
docker run -d nginx
docker run -p 8080:80 nginx
docker exec -it <container> bash
docker build -t myapp .
docker volume create myvolume
docker compose up
docker compose down
docker system prune
```
