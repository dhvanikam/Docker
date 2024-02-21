# Docker Hub

Docker Hub is a cloud-based registry service provided by Docker that allows you to store and share Docker container images. It serves as a central repository for Docker images, making it easy for developers to share and distribute their containerized applications. Docker Hub is widely used in the Docker community, and it provides a convenient platform for collaboration and distribution of containerized applications.

You can create a free Docker account with your email address or by signing up with your Google or GitHub account. Once you've created your account with a unique Docker ID, you can access all Docker products, including Docker Hub. 

https://docs.docker.com/docker-id/


Here are some key features and aspects of Docker Hub:

1. **Image Repository:**
   - Docker Hub hosts a vast collection of public Docker images that cover a wide range of applications and services. These images are available for anyone to use.

2. **User Accounts:**
   - Users can create accounts on Docker Hub to publish their own Docker images, collaborate with others, and manage their repositories.

3. **Private Repositories:**
   - Docker Hub offers both public and private repositories. Public repositories are visible to everyone, while private repositories require authentication to access.

4. **Automated Builds:**
   - Docker Hub supports automated builds, allowing you to connect your source code repositories (such as GitHub) to Docker Hub. When you push changes to your source code, Docker Hub automatically triggers a new build of your Docker image.

5. **Web Interface:**
   - Docker Hub provides a web interface where you can search for Docker images, explore repositories, and manage your own images and repositories.

6. **Docker Hub CLI:**
   - Docker Hub also provides a command-line interface (CLI) that allows you to interact with Docker Hub from your local machine using Docker commands.

To access Docker through the command line interface (CLI), you need to use the `docker` command followed by various subcommands to perform different actions such as managing containers, images, volumes, networks, and more. Here are some commonly used Docker commands:

1. **Docker version:**
   ```bash
   docker version
   ```
   This command shows the Docker client and server version information.

2. **Docker info:**
   ```bash
   docker info
   ```
   This command displays system-wide information about Docker and its components.

3. **Pull an image from Docker Hub:**
   ```bash
   docker pull <image_name>
   ```
   This command downloads a Docker image from Docker Hub.

4. **List Docker images:**
   ```bash
   docker images
   ```
   This command lists all Docker images stored locally on your system.

5. **Run a container:**
   ```bash
   docker run <image_name>
   ```
   This command creates and starts a new container from a specified image.

6. **List running containers:**
   ```bash
   docker ps
   ```
   This command lists all currently running Docker containers.

7. **List all containers (including stopped ones):**
   ```bash
   docker ps -a
   ```
   This command lists all Docker containers, including those that are stopped.

8. **Stop a container:**
   ```bash
   docker stop <container_id>
   ```
   This command stops a running container.

9. **Start a stopped container:**
   ```bash
   docker start <container_id>
   ```
   This command starts a stopped container.

10. **Remove a container:**
    ```bash
    docker rm <container_id>
    ```
    This command removes a stopped container.

11. **Remove an image:**
    ```bash
    docker rmi <image_id>
    ```
    This command removes a Docker image from your local repository.

12. **Inspect a container:**
    ```bash
    docker inspect <container_id>
    ```
    This command provides detailed information about a container.

13. **Execute a command in a running container:**
    ```bash
    docker exec -it <container_id> <command>
    ```
    This command executes a command inside a running container.

14. **View logs of a container:**
    ```bash
    docker logs <container_id>
    ```
    This command displays the logs of a specific container.

These are some of the most commonly used Docker commands. We can use them to manage Docker containers, images, volumes, networks, and other resources on your system.
