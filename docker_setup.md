# Install Docker Engine on your WSL Ubuntu

To install Docker Engine, you need the 64-bit version of one of these Ubuntu versions:
- Ubuntu Oracular 24.10
- Ubuntu Noble 24.04 (LTS)
- Ubuntu Jammy 22.04 (LTS)

## Install using the apt repository
Before you install Docker Engine for the first time on a new host machine, you need to set up the Docker `apt` repository. Afterward, you can install and update Docker from the repository.

```bash

# Update and install requirements
sudo apt update
sudo apt install -y ca-certificates curl gnupg lsb-release

# Add Docker GPG key
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

# Add Docker repository
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

# Install Docker Engine + CLI
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

# Start Docker service
sudo service docker start

# (Optional) This would allow you to Run docker without `sudo`
sudo usermod -aG docker $USER
```

## Some useful docker commands
```bash
# List running containers
docker ps

# List all containers (including stopped)
docker ps -a

# Stop a container
docker stop my_container_name

# Start a stopped container
docker start my_container_name

# Remove a container
docker rm my_container_name
```
## Some commands for dealing with images
```bash
# List downloaded images
docker images

# Download (pull) an image
docker pull python:3.11

# Remove an image
docker rmi python:3.11

# Build an image from a Dockerfile
docker build -t myapp:latest .
```


