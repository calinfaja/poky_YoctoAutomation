
# Jenkins Automation for Yocto Project: Building QEMU on Docker

## 1. Setting up GitHub Repo

## 2. Setting up Docker Containers
Structure for the moment:

    /ppyocto 
    ├── docker-compose.yml 
    ├── Dockerfile 
    ├── ubuntu-builder/ 
    ├── workspace/ # This directory should exist and contain your files 
    	└── setup_yocto_build.sh

## Container for building Yocto
Container name: ubuntu-container
Dependencies installed from [YoctoQuickBuild Page](https://docs.yoctoproject.org/brief-yoctoprojectqs/index.html)
Script for cloning repo and building dunfell QEMU Image: **setup_yocto_build.sh**

**Useful docker commands:**
`docker-compose down`  # Stop and remove the container
`docker-compose build` # Build the container
`docker-compose up --build -d`  # Rebuild and start the container
`docker exec -it ubuntu-container bash` # Enter the container
(bash) `dpkg -l | grep -E "gawk|git|texinfo|python3|xz-utils|file"`   Check installed packages 
(bash) `ssh root@localhost -p 2222`

## Container for Jenkins
Docker ensures a consistent and isolated build environment. Steps:

1. Install Docker on your host machine.
2. Create a `Dockerfile` for your Yocto project. Example:
   ```dockerfile
   FROM ubuntu:20.04

   RUN apt-get update && apt-get install -y \
       git \
       build-essential \
       qemu \
       && rm -rf /var/lib/apt/lists/*

   WORKDIR /yocto

## 3. Setting up Jenkins Automation
Jenkins will be used to automate the build process. Here's how to set it up:

1. Install Jenkins on your system or use a cloud-hosted Jenkins service.
2. Install required plugins, such as:
   - **Git Plugin**: For cloning the repository.
   - **Pipeline Plugin**: To manage complex build steps.
   - **Docker Plugin**: To run builds inside Docker containers.
3. Create a new pipeline job and configure it to clone the GitHub repository.
4. Define the pipeline script (`Jenkinsfile`) in the repository with stages for fetching dependencies, setting up the environment, and triggering the build.


