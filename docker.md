# Docker

## Table of Contents

0. **Introduction to Containers**

1. **Introduction to Docker**
   - Definition and Overview
   - Docker Architecture
     - Docker Daemon
     - Docker Client
     - Docker Registries
   - Core Concepts and Components
     - Images
     - Containers
     - Dockerfiles
   - Advantages of Using Docker
     - Isolation
     - Portability
     - Efficiency

2. **Docker Installation and Configuration**
   - Installing Docker on Various Platforms
   - Post-installation Steps
   - Configuring Docker for Best Performance
   - Docker Version Management

3. **Working with Docker Images**
   - Understanding Docker Images
   - Building Images with Dockerfile
     - Dockerfile Syntax and Instructions
     - Best Practices for Writing Dockerfiles
   - Managing Images
     - Listing, Tagging, and Removing Images

4. **Docker Containers**
   - Basics of Docker Containers
   - Creating, Starting, and Stopping Containers
   - Container Management
     - Inspecting, Monitoring, and Logging
     - Executing Commands in a Running Container
   - Container Networking
     - Overview of Networking in Docker
     - Network Types
     - Connecting Containers
     - Port Mapping and Exposing Services
   - Data Management in Containers
     - Volumes
     - Bind Mounts
     - tmpfs Mounts
     - Data Persistence and Sharing
   - Docker Compose: Multi-container Applications
     - YAML File Structure
     - Defining and Running Multi-container Applications

5. **Docker Volumes**
   - Understanding Docker Volumes
   - Creating and Managing Volumes
   - Volume Drivers and Plugins
   - Backup, Restore, and Migrating Data Volumes

6. **Docker Networking**
   - Deep Dive into Docker Networking
   - Custom Network Creation
   - Inspecting and Troubleshooting Networks
   - Docker Network Commands

7. **Docker Security**
   - Overview of Docker Security
   - Container Security Best Practices
   - Docker Daemon Security
   - Network Security in Docker
   - Managing Secrets in Docker
     - Using Docker Secrets
     - Best Practices for Secret Management

8. **Advanced Docker Topics**
   - Docker Swarm: Clustering and Orchestration
   - Docker Engine API
   - Continuous Integration/Continuous Deployment (CI/CD) with Docker

9. **Troubleshooting and Best Practices**
   - Common Docker Issues and Solutions
   - Performance Tuning and Optimization
   - Dockerfile and Image Optimization
   - Security Scanning and Audits
  
## 0. Introduction to Containers

Understanding the differences between physical machines, virtual machines (VMs), and containers is crucial for grasping the evolution of virtualization and containerization technologies. Each approach offers unique advantages and serves different use cases in the realm of computing resources management.

**Physical Machines** :A physical machine (PM) is a standard computer with its hardware components, including CPU, memory, storage, and network resources. It runs an operating system (OS) directly on its hardware without any virtualization layer.

- Performance: Offers the highest performance as it directly utilizes the hardware without any overhead. However, this also means that resource allocation is fixed and less flexible.
- Isolation: Each physical machine is naturally isolated by its hardware, leading to increased security and stability but at the cost of scalability and efficiency.
- Use Cases: Ideal for applications requiring maximum performance and hardware access, such as high-performance computing (HPC) tasks.

**Virtual Machines**: VMs are emulated environments created by virtualization software (hypervisors) running on physical machines. Each VM includes a full copy of an operating system, a virtual copy of the hardware that the OS requires to run, and the application and its dependencies.

- Performance: Introduces a performance overhead due to the hypervisor layer but provides significant flexibility in resource allocation and scalability.
- Isolation: Offers strong isolation since each VM is completely separate from others and the host system. This makes VMs suitable for running multiple different applications on the same physical hardware securely.
- Use Cases: Suited for consolidating multiple server roles on a single physical machine, legacy application compatibility, and environments requiring strong isolation between running applications.

**Containers**: Containers provide a lightweight form of virtualization, packaging an application and its dependencies into a single executable package. Unlike VMs, containers share the host OS kernel but maintain isolation through namespaces and control groups.

- Performance: Containers start faster and use fewer resources than VMs because they don't include guest OS instances. This efficiency supports high-density deployment and microservice architectures.
- Isolation: While containers are isolated from each other and the host system, they are considered less isolated than VMs since they share the host OS kernel. However, advancements in container security technologies continue to improve their isolation capabilities.
- Use Cases: Ideal for microservices, cloud-native applications, and any scenario where application portability, scalability, and efficient resource utilization are desired.

**Summary**

- Resource Efficiency: Containers offer the highest resource efficiency, followed by VMs, with physical machines being the least efficient in terms of resource utilization.
- Startup Time: Containers have the quickest startup time, VMs are slower, and physical machines have the longest boot times due to their reliance on hardware initialization.
- Portability: Containers excel in portability across different environments, VMs offer moderate portability, and physical machines are the least portable.
- Isolation and Security: Physical machines provide the highest level of security and isolation, followed by VMs. Containers, while still secure, share the host OS kernel, which presents a different security model.

# 1. Introduction to Docker

## Definition and Overview

Docker is an open-source platform that automates the deployment, scaling, and management of applications within software containers. It provides an additional layer of abstraction and automation of operating-system-level virtualization on Linux and Windows.

Docker containers are lightweight, stand-alone, executable packages that include everything needed to run a software application: code, runtime, system tools, libraries, and settings.

## Docker Architecture

- **Docker Daemon**: The background service running on the host that manages building, running, and distributing Docker containers. The daemon is the process that executes Docker commands issued by the Docker client.
- **Docker Client**: The command line tool that allows the user to interact with the Docker daemon. Through Docker client, users can issue a wide range of commands to launch, stop, and manage containers.
- **Docker Registries**: Centralized platforms that store and distribute Docker images. Docker Hub is the default registry where Docker looks for images, but users can configure their own private registries or use third-party options.

## Core Concepts and Components

- **Images**: Read-only templates used to create containers. Images include the application code, libraries, tools, dependencies, and other files needed to run an application. Docker images are built from Dockerfiles and stored in a registry.
- **Containers**: Runnable instances of Docker images. Containers run the application and its dependencies in an isolated environment. They can be started, stopped, moved, and deleted.
- **Dockerfiles**: Text documents that contain all the commands a user could call on the command line to assemble an image. Docker can build images automatically by reading the instructions from a Dockerfile.

## Advantages of Using Docker

- **Isolation**: Docker ensures that applications run in isolated environments called containers, preventing conflicts between applications and between applications and the host system.
- **Portability**: Since Docker containers include everything needed to run an application, they can be moved easily between environments, ensuring consistency across development, testing, and production.
- **Efficiency**: Containers share the host system's kernel, making them much more efficient in terms of system resources than traditional virtual machines that require a full operating system for each instance.

# 2. Docker Installation and Configuration

Proper installation and configuration of Docker are critical steps to ensure its effective use for development, testing, and production environments. This section covers the essential steps to get Docker up and running on various platforms, along with tips for optimizing its performance.

## Installing Docker on Various Platforms

Docker is supported on several operating systems, including Linux, Windows, and macOS. The installation process varies depending on the platform. Follow the instructions on the Docker website.

## Post-installation Steps

After installing Docker, consider these post-installation steps to enhance security and functionality:

- **Manage Docker as a non-root user**: Running Docker as a non-root user improves the security of your system by reducing the potential attack surface. This configuration prevents unauthorized access to critical system files and limits the damage that could result from a compromised container or Docker daemon. Create a Docker group and add your user to it to avoid using Docker as the root user.
  
   1. Create the Docker Group

        ```bash
        sudo groupadd docker
        ```

   2. Add Your User to the Docker Group

        ```bash
        sudo usermod -aG docker <your-user>
        ```

   3. Activate the Group Membership

        ```bash
        newgrp docker
        ```

   4. Test Docker without Sudo

        ```bash
        docker run hello-world
        ```

- **Configure Docker to start on boot**: Automatically starting Docker on boot ensures that Docker services and containers are promptly available after a system restart, which is crucial for maintaining service availability in production environments. Most Docker installations will set Docker to start on boot by default. This behavior can be adjusted as needed.

    ```bash
    sudo systemctl enable docker
    ```

## Configuring Docker for Best Performance

Configuring Docker properly can significantly affect its performance. Some tips include:

- **Resource Allocation**: Adjust the CPU and memory allocation in Docker's settings (especially for Docker Desktop) to match your workload requirements.
- **Storage Drivers**: The choice of storage driver affects the performance and efficiency of Docker containers by determining how they read, write, and store data. Selecting the appropriate driver can significantly improve container performance and resource utilization. Choose the appropriate storage driver for your environment. Overlay2 is recommended for Linux systems for its performance and compatibility.

  1. Configure Docker to Use Overlay. Edit the Docker daemon configuration file, usually located at `/etc/docker/daemon.json`, to specify `Overlay2` as the storage driver.

     ```json
     {
      "storage-driver": "overlay2"
      }
     ```

  2. Restart Docker to apply the changes.

     ```bash
     sudo systemctl restart docker
     ```

- **Network Settings**: For complex networking needs, consider customizing Docker's default network settings, such as creating user-defined bridges for better isolation and network performance.

  1. Create a Bridge Network

        ```bash
        docker network create --driver bridge my_bridge
        ```

  1. Run Containers on the Custom Network

        ```bash
        docker run --network=my_bridge -d <image-name>
        ```

# 3. Working with Docker Images

Dockerfiles create images, images create containers.

**Dockerfile**: A Dockerfile is a text document containing all the commands needed to build an image.

**Images**: Docker images are immutable templates used to create containers. They are built from a series of layers that represent instructions in a Dockerfile, making it easy to share and version-control your application environments.

**Image Layers**: When an image is built, each instruction in the Dockerfile creates a new layer. Docker uses a union file system to stack these layers, allowing for efficient storage and quick sharing of common layers between images.

Here is an example Dockerfile:

```Dockerfile
# Use an official Python runtime as a parent image
FROM python:3.8-slim

# Set the working directory in the container
WORKDIR /app

# Copy the current directory contents into the container at /app
COPY . .

# Install any needed packages specified in requirements.txt
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# Make port 80 available to the world outside this container
EXPOSE 80

# Define environment variable
ENV NAME World

# Run app.py when the container launches
CMD ["python", "app.py"]
```

We can build an image from a dockerfile, then run it, then enter into the container:

```bash
docker build -t my-python-app .
docker run my-python-app
docker exec my-python-app
```

### Dockerfile Instructions

- `FROM`: Sets the base image for subsequent instructions. For example, `FROM ubuntu:18.04`.
- `LABEL`: Adds metadata to an image, such as maintainer, version, or description.
- `ENV`: Sets environment variables within the image. For instance, `ENV PATH /usr/local/bin:$PATH`.
- `RUN`: Executes commands in a new layer on top of the current image and commits the results.
- `CMD`: Provides defaults for an executing container. If Docker container runs with arguments, the CMD is ignored.
- `EXPOSE`: Informs Docker that the container listens on specific network ports at runtime.
- `ENV`: Sets environment variables.
- `ADD`: Copies new files, directories, or remote file URLs from `<src>` and adds them to the filesystem of the image at the path `<dest>`.
- `COPY`: Copies new files or directories from `<src>` and adds them to the filesystem of the container at the path `<dest>`.
- `ENTRYPOINT`: Configures a container that will run as an executable.
- `VOLUME`: Creates a mount point with the specified name and marks it as holding externally mounted volumes from native host or other containers.
- `USER`: Sets the username or UID to use when running the image and for any `RUN`, `CMD`, and `ENTRYPOINT` instructions that follow it.
- `WORKDIR`: Sets the working directory for any `RUN`, `CMD`, `ENTRYPOINT`, `COPY`, and `ADD` instructions that follow it.
- `ARG`: Defines a variable that users can pass at build-time to the builder with the `docker build` command.
- `ONBUILD`: Adds a trigger instruction to be executed at a later time, when the image is used as the base for another build.
- `STOPSIGNAL`: Sets the system call signal that will be sent to the container to exit.
- `HEALTHCHECK`: Tells Docker how to test a container to check that it is still working.
- `SHELL`: Allows the default shell used for the shell form of commands to be overridden.

### A Few Docker Commands

- `docker build -t my-image:tag .`: Builds a Docker image from a Dockerfile in the current directory, tagging it with a name and tag.
- `docker images`: Lists all Docker images on the host.
- `docker run -d --name my-container my-image:tag`: Runs a container from the specified image in detached mode with a name.
- `docker ps`: Lists currently running containers.
- `docker ps -a`: Lists all containers, including stopped ones.
- `docker exec -it my-container bash`: Executes an interactive bash shell inside the running container.
- `docker stop my-container`: Stops a running container.
- `docker rm my-container`: Removes a stopped container.
- `docker rmi my-image:tag`: Removes an image.
- `docker logs my-container`: Fetches the logs of a container.
- **Creating Containers**: Use `docker create` with an image name to create a container without starting it.
- **Starting Containers**: Use `docker start` followed by the container ID or name to start a container.
- **Stopping Containers**: Use `docker stop` followed by the container ID or name to gracefully stop a running container.
- **Executing Commands**: `docker exec -it [container_id] [command]` allows you to run commands inside a running container, such as opening a bash shell with `docker exec -it [container_id] bash`.

## Networking

Docker networking enables isolated containers to communicate with each other and the external network while maintaining a high level of security. Each container has its own networking namespace, meaning it has a unique IP address, routing table, and set of network interfaces.

Docker supports multiple network drivers, each designed for specific use cases:

Bridge: The default network driver for containers. When a container is launched without specifying a network, it's automatically attached to a default bridge network. This network is private and internal to the host machine, allowing containers connected to the same bridge network to communicate while isolating them from other networks.

Host: This driver removes network isolation between the container and the Docker host, allowing containers to use the host’s networking directly. Containers using the host network can open any port on the host machine without port mappings, offering better performance for high-traffic applications but less isolation.

Overlay: Used in Docker Swarm mode to enable containers running on different Docker hosts to communicate as if they were on the same host. Overlay networks require some additional setup, including a key-value store for network state management and a Swarm cluster.

Macvlan: Allows you to assign a MAC address to a container, making it appear as a physical device on your network. Containers can communicate with the network without passing through the Docker host's network stack. This is useful for applications that expect to be directly connected to the physical network.

None: Disables all networking for a container. This is useful when you want to completely isolate a container's networking.

Docker Embedded DNS
Docker’s embedded DNS server (available in user-defined networks, not in the default bridge network) allows containers to resolve other containers’ names to their IP addresses. When a container is connected to multiple networks, it can resolve names of containers in any of those networks, facilitating communication between services on different networks.

Best Practices
Use Custom Bridge Networks: For better isolation and easier container-to-container communication, prefer creating custom bridge networks over using the default bridge.

Secure Overlay Networks: When using overlay networks, especially across multiple hosts, ensure you secure your network communication with encryption.

Avoid Host Networking Unless Necessary: While host networking offers performance benefits, it reduces isolation. Use it only when necessary, such as for high-performance web servers or proxies.

Plan IP Addressing: For complex applications, especially on custom or overlay networks, plan your IP addressing scheme to avoid conflicts and ensure clear communication paths.

## Persistance

### Volumes

Docker volumes are the preferred mechanism for persisting data generated by and used by Docker containers. They are completely managed by Docker and are isolated from the core functioning of the host machine, which makes them safe and convenient.

Data in volumes persists beyond the lifecycle of a single container. Volumes are portable and can be easily backed up, shared, or migrated than other storage options. Volumes are isolated from the host system.

### Bind Mounts

Bind mounts are a simple way to persist data in Docker containers by mapping a host file or directory to a container file or directory. Essentially, a bind mount allows a container to access and modify files on the host machine.

They provides direct access to the host’s filesystem and are useful for development environments where code or data needs to be live-reloaded.

### tmpfs Mounts

tmpfs mounts allow you to mount a temporary file storage in the memory of the host machine for use by a container. This storage is very fast but does not persist data to disk.
