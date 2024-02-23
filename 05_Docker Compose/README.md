# Docker Compose

![DockerCompose1 drawio](https://github.com/dhvanikam/Docker/assets/73573915/8e381100-e95d-4771-b2fe-c4caab8598ea)

Docker Compose is a tool for defining and running multi-container applications. It is the key to unlocking a streamlined and efficient development and deployment experience.

Compose simplifies the control of your entire application stack, making it easy to manage services, networks, and volumes in a single, comprehensible YAML configuration file. Then, with a single command, you create and start all the services from your configuration file.

Compose works in all environments; production, staging, development, testing, as well as CI workflows. It also has commands for managing the whole lifecycle of your application:

Start, stop, and rebuild services
View the status of running services
Stream the log output of running services
Run a one-off command on a service

An important part of any Continuous Deployment or Continuous Integration process is the automated test suite. Automated end-to-end testing requires an environment in which to run tests. Compose provides a convenient way to create and destroy isolated testing environments for your test suite. By defining the full environment in a Compose file, you can create and destroy these environments in just a few commands:


 docker compose up -d
 ./run_tests
 docker compose down

## Installation
For Windows and macOS
* Docker Compose is included in Docker Desktop for Windows and macOS.

OR Go to https://docs.docker.com/compose/install/

## Using Docker Compose is a three-step process:

* Define the services that make up your app in compose.yaml so they can be run together in an isolated environment.
* Lastly, run docker compose up and Compose will start and run your entire app.
* After tests are done, To stop the Grid and cleanup the created containers, run docker-compose down.

Version 2
docker-compose-v2.yml : https://github.com/SeleniumHQ/docker-selenium/blob/trunk/docker-compose-v2.yml

Version 3
docker-compose-v3.yml : https://github.com/SeleniumHQ/docker-selenium/blob/trunk/docker-compose-v3.yml
* For Windows and Linux no need to change any image names in yml file.

* For my system macOS ARM64, i have to use specific hub and node images so need to update,
```yml
# To execute this docker-compose yml file use `docker-compose -f docker-compose-v3.yml up
# Add the `-d` flag at the end for detached execution
# To stop the execution, hit Ctrl+C, and then `docker-compose -f docker-compose-v3.yml down
version: "3"
services:
  chrome:
    image: seleniarm/node-chromium
    shm_size: 2gb
    depends_on:
      - selenium-hub
    environment:
      - SE_EVENT_BUS_HOST=selenium-hub
      - SE_EVENT_BUS_PUBLISH_PORT=4442
      - SE_EVENT_BUS_SUBSCRIBE_PORT=4443

  firefox:
    image: seleniarm/node-firefox
    shm_size: 2gb
    depends_on:
      - selenium-hub
    environment:
      - SE_EVENT_BUS_HOST=selenium-hub
      - SE_EVENT_BUS_PUBLISH_PORT=4442
      - SE_EVENT_BUS_SUBSCRIBE_PORT=4443

  selenium-hub:
    image: seleniarm/hub
    container_name: selenium-hub
    ports:
      - "4442:4442"
      - "4443:4443"
      - "4444:4444"
```

**version 3**: It is the latest version of the docker-compose files.

**services(containers)**: This contains the list of the images and their configurations.

**image**: It defines which image will be used to spin up container.

**shm_size**: Use the host's shared memory.

**ports**: Published ports in exposed port : container port format.

**container_name**: Name of our containers.

**depends_on**: This defines the required dependency before spinning up the container. In our docker-compose.yml file, containers Chrome and Firefox are dependent upon container hub to spin up.

**SE_EVENT_BUS_HOST**: Hub host.

**SE_EVENT_BUS_PUBLISH_PORT** and **SE_EVENT_BUS_SUBCRIBE_PORT**:  Ports 4442 and 4443 are exposed by default for Event Bus ports to help them communicate with Hub.
