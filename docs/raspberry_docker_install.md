sudo apt update
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://get.docker.com -o get-docker.sh
sudo usermod -aG docker $USER
docker --version
sudo apt install -y libffi-dev libssl-dev python3 python3-pip
docker-compose --version
docker ps
docker ps -a
docker images
docker start <container_name_or_id>
docker stop <container_name_or_id>
docker rm <container_name_or_id>
docker rmi <image_name_or_id>
docker logs <container_name_or_id>
docker stats
docker exec -it <container_name_or_id> bash
docker stats
or
top

# Docker Installation and Common Commands on Raspberry Pi

This guide explains how to install Docker on a Raspberry Pi, along with some common commands to manage containers and images. You can use this on multiple Pis for quick setup.

---

## 1. Update Raspberry Pi

```sh
sudo apt update
sudo apt upgrade -y
sudo reboot
```

---

## 2. Install Required Packages

```sh
sudo apt install -y apt-transport-https ca-certificates curl software-properties-common
```

---

## 3. Install Docker

Use the official Docker convenience script:

```sh
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
```

---

## 4. Add User to Docker Group (Optional)

So you can run Docker commands without sudo:

```sh
sudo usermod -aG docker $USER
```

Then either log out and log back in, or run:

```sh
newgrp docker
```

---

## 5. Verify Docker Installation

```sh
docker --version
docker run hello-world
```

Expected output: “Hello from Docker!” confirming Docker is installed correctly.

---

## 6. Install Docker Compose (Optional)

Install dependencies and Docker Compose for ARM architecture:

```sh
sudo apt install -y libffi-dev libssl-dev python3 python3-pip
sudo pip3 install docker-compose
```

Verify:

```sh
docker-compose --version
```

---

## 7. Useful Docker Commands

**List running containers**

```sh
docker ps
```

**List all containers (running + stopped)**

```sh
docker ps -a
```

**List all images**

```sh
docker images
```

**Start a container**

```sh
docker start <container_name_or_id>
```

**Stop a container**

```sh
docker stop <container_name_or_id>
```

**Remove a container**

```sh
docker rm <container_name_or_id>
```

**Remove an image**

```sh
docker rmi <image_name_or_id>
```

**View container logs**

```sh
docker logs <container_name_or_id>
```

**View real-time resource usage**

```sh
docker stats
```

**Execute a command inside a running container**

```sh
docker exec -it <container_name_or_id> bash
```

---

## Notes & Tips

- Pi 3B+ has 1 GB RAM, so avoid running too many containers at once.
- Use headless mode / Lite OS to save resources.
- Monitor memory usage using:

	```sh
	docker stats
	```

	or

	```sh
	top
	```

	for overall system usage.
- Keep Docker updated via the convenience script or apt upgrade regularly.

---

This file can be copied to multiple Raspberry Pis and followed step-by-step to set up Docker and basic management commands.