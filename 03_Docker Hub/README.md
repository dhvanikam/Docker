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

   Example :
    ```bash
   docker pull selenium/standalone-chrome
   ```

4. **List Docker images:**
   ```bash
   docker images
   ```
   This command lists all Docker images stored locally on your system.
   Example :
   <img width="768" alt="dockerimages" src="https://github.com/dhvanikam/Docker/assets/73573915/e0af2bf2-1d23-4750-9f2d-5470e19d5efb">


5. **Run a container:**
   ```bash
   docker run <image_name>
   ```
    
   This command creates and starts a new container from a specified image.We will see more in details in next topic.
   Example :
    ```bash
   docker run -d -p 4444:4444 selenium/standalone-chrome
   ```
   <img width="949" alt="dockerrun" src="https://github.com/dhvanikam/Docker/assets/73573915/07569b97-7b42-4213-9d0c-7e8b2b63f1e4">

   

6. **List running containers:**
   ```bash
   docker ps
   ```
   This command lists all currently running Docker containers.
   Example:
   <img width="1235" alt="dockerps" src="https://github.com/dhvanikam/Docker/assets/73573915/fa94c1de-5af5-482d-88cf-f8e16bd886b3">

   Note the Container ID

7. **List all containers (including stopped ones):**
   ```bash
   docker ps -a
   ```
   This command lists all Docker containers, including those that are stopped.

   Example:
   <img width="1348" alt="dockerps-a" src="https://github.com/dhvanikam/Docker/assets/73573915/99a2d53a-4d02-41dc-bb32-026eae627354">

8. **Inspect a container:**
    ```bash
    docker inspect <container_id noted previously>
    ```
    This command provides detailed information about a container.
    Example:
    <img width="763" alt="dockerinspect" src="https://github.com/dhvanikam/Docker/assets/73573915/b47aa008-8e6a-40fb-9e6c-7e597e366f53">


9. **Execute a command in a running container:**
    ```bash
    docker exec -it <container_id noted previously> <command>
    ```
    This command executes a command inside a running container.
    Example:
    <img width="1354" alt="dockerexcecmnd" src="https://github.com/dhvanikam/Docker/assets/73573915/7bd82603-1ac9-4d23-99f9-51d14983f0ee">


10. **View logs of a container:**
    ```bash
    docker logs <container_id noted previously>
    ```
    This command displays the logs of a specific container.
    Example:
    <img width="848" alt="dockerlogs" src="https://github.com/dhvanikam/Docker/assets/73573915/4ccad046-0160-4081-b551-2a3680b72c81">

11. **Stop a container:**
    ```bash
    docker stop <container_id noted previously>
    ```
    This command stops a running container.
    Example:
    <img width="758" alt="Dockerstop" src="https://github.com/dhvanikam/Docker/assets/73573915/ae7e64bd-c4c5-42ed-93f5-c908c0cfd69d">


12. **Start a stopped container:**
    ```bash
    docker start <container_id noted previously>
    ```
    This command starts a stopped container.
    Example:
    <img width="1243" alt="dosckerstart" src="https://github.com/dhvanikam/Docker/assets/73573915/9553cfc4-b28e-4e18-a79f-84df6973040c">


13. **Remove a container:**
    ```bash
    docker rm <container_id noted previously>
    ```
    This command removes a stopped container.

    Example:
    <img width="1243" alt="Dockerremove" src="https://github.com/dhvanikam/Docker/assets/73573915/f5e50f43-19c7-478b-9bd6-31b817365f75">


14. **Remove an image:**
    ```bash
    docker rmi <image_id noted from "docker images" command>
    ```
    This command removes a Docker image from your local repository.
    Example:
    

These are some of the most commonly used Docker commands. We can use them to manage Docker containers, images, volumes, networks, and other resources on your system.
