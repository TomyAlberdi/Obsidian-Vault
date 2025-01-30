Created: 2024-09-17 16:24
## Family Tree:
1. Computer
2. [[Infrastructure Administration]]
-- -
Docker is an open-source project that automates the deployment of applications within software containers. It provides an additional layer of abstraction and automation for application virtualization across different operating systems.
In essence, Docker is a simplified way to package and run applications. With Docker installed on any system, it can be up and running within minutes, offering ease in building, running, stopping, starting, inspecting, modifying, and managing containers. This technology also makes deploying applications more efficient in cloud environments. Since containers include most of what they need to run, the operating systems that host them can be slimmed down.
"Containerized" applications can run anywhere, on anything. By encapsulating dependencies, Docker allows developers and system administrators to work together more effectively. Containers help isolate resources, restrict services, and give processes a nearly private view of the operating system, including their own process ID space, filesystem structure, and network interfaces.
Docker simplifies the creation of highly distributed systems by allowing you to quickly deploy and manage containers.
## Key benefits:
- **Simplifies workload creation**: Docker makes it easier to create and manage workloads.
- **Optimizes workload operations**: It enhances efficiency in running workloads.
## Docker Platform Components:
- **Docker Engine / Docker Daemon**:  
  This is the core program that allows you to build, ship, and run containers. It uses Linux kernel features such as namespaces and control groups (`cgroups`) to provide an isolated runtime environment for each application.
- **Docker Hub**:  
  An online registry of Docker images, where you can find, share, and store container images.
- **Docker Trusted Registry**:  
  A private, on-premises registry for storing and managing Docker images securely.
- **Docker Client**:  
  The interface through which users issue commands, which are then sent to the Docker daemon. The client and daemon can run on the same or different hosts.
- **Docker Images**:  
  Read-only templates used to create containers. They contain a set of instructions on how to build a containerized environment.
- **Docker Containers**:  
  These are isolated application environments based on one or more Docker images. They contain everything necessary to run an application, including code, dependencies, and configurations.
## Dockerfile
A **Dockerfile** is a simple text file that contains a set of commands or instructions. These commands are executed sequentially to perform actions on a base image to create a new Docker image.
### Basic Instructions:
- **`FROM`**: Defines the base image to use and starts the build process.
- **`RUN`**: Takes a command and its arguments to execute it in the image.
- **`CMD`**: Similar to `RUN`, but only executes after the container is instantiated. It sets default commands or arguments that can be overridden when the container runs.    
- **`ENTRYPOINT`**: Specifies the default application to run when a container is created from the image.    
- **`ADD`**: Copies files from a source path to a destination inside the container.
- **`ENV`**: Sets environment variables in the container.
### Image Tags:
Tags are used to identify image versions. When listing images, each one appears with its associated tag. You can group your images using names and tags. If no tag is provided, the default `latest` tag is assumed.
## Docker Compose
Docker Compose is a tool that simplifies the use of Docker. Using YAML files, it becomes easier to create containers, connect them, enable ports, manage volumes, and more. With Compose, you can create multiple containers and, within each container, different services, link them to a shared volume, start and stop them, and manage complex setups easily. It is a fundamental component for building applications and microservices.
Instead of relying on a series of hard-to-remember Bash commands and scripts, Docker Compose allows you to instruct the Docker Engine programmatically through YAML files. This is the key advantage: the ability to give a series of instructions and then repeat them across different environments.
### Benefits:
- **No Additional Software**: 
  There is no need to install or maintain additional software on your system.
- **Centralized Development Environment**:  
  You can keep your entire development environment (back end, front end, database configurations, etc.) in a single repository, which makes collaboration between developers easier.
- **Single Command Setup**:  
  Bringing up the entire development environment is as simple as running one command: `docker-compose up`.
### Downsides:
One drawback of Docker Compose is related to **performance**. While containers are designed to be efficient, they still consume resources from the host machine, such as CPU and memory. If you run a large number of containers simultaneously or if the containers are resource-heavy, it could lead to system slowdowns or crashes.
### Flexibility for Testing:
Docker Compose allows you to test with different environments and languages, helping you optimize your development setup. This lets you focus on the primary goal: writing quality code.
## Good Practices
### Using official images:
On Docker Hub, there are two types of images: official ones, published by organizations (e.g., Ubuntu), and user-published images. Official images are labeled as such on Docker Hub. For example, if you search for Ubuntu, you'll see images published by Canonical tagged as **Docker Official Image**.
The easiest way to differentiate between official and non-official images is by their names:
- **Official Image**: `docker pull ubuntu:latest`
- **Non-official Image**: `docker pull user/nginx:latest`
Non-official images may contain modifications that aren't immediately clear, such as additional packages or altered configurations.
### Using `COPY` instead of `ADD`:
Both `COPY` and `ADD` allow copying files into Docker images, but there are differences:
- **ADD**: Supports copying files from multiple sources (e.g., local filesystem, web-hosted files) and can automatically unpack `.tar` files. However, it can cause confusion due to its multifunctionality.
- **COPY**: Designed specifically to copy files from the local filesystem to the image, making Dockerfiles easier to read and more predictable.
**Recommendations**:
- Use **COPY** for copying local files during the build process.
- Use **RUN** with `curl` or similar tools to download files from the web and then copy or extract them.
- Use **ADD** when you need to automatically unpack `.tar` files.
### Multi-stage Builds:
Multi-stage builds allow you to create smaller Docker images by explicitly including only the necessary components. In a multi-stage build, the Dockerfile has multiple `FROM` instructions:
- The first stage may use a base image to compile your code.
- The second stage uses a minimal base image with only the dependencies required to run the application.
This technique helps reduce the size of the final image, as it eliminates unnecessary build tools and artifacts.
### Avoid external dependencies:
Containers should be self-sufficient and portable. While it may be tempting to mount local directories into a container during development to speed up the process, this can lead to unresolved dependencies in production.
Contrary to some Docker development practices (like using bind mounts in development environments), it’s recommended not to rely on external volumes during development to avoid issues in production.
### Concatenating commands:
Each `RUN` command in a Dockerfile creates a new image layer. Concatenating related commands reduces the number of layers and improves resource usage and build times. For example:
```dockerfile
RUN apt-get update && apt-get upgrade -y
```
This is better than separating them into two `RUN` commands, as it serves the same purpose and optimizes image creation.