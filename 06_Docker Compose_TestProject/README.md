# Docker Compose Example

Find sample Project on : https://github.com/dhvanikam/DockerSampleProject 

We have 

Step 1: Point RemoteWebDriver in your test to http://localhost:4444 



Step 2: Update TestNG.xml as we show last,


Step 2: Go to your project directory where "docker-compose-v2.yml" is residing

Run the docker compose file
To execute this docker-compose yml file use

docker-compose -f docker-compose-v2.yml up
Add the -d flag at the end for detached execution

docker-compose -f docker-compose-v2.yml up -d
