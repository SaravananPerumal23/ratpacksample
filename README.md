# Ratpacksample with Jenkins Pipeline 
Sample Ratpack app with Docker, jenkins pipeline setup, Unit test, Selenium test, Sonarqube integration


## Ratpack App
Simple Web API using Ratpack framework

#### Building project
```
./gradlew build
```
#### Running project
```
./gradlew run
```
(or)
```
java -jar my.ratpackapp-1.0-SNAPSHOT-all.jar
```

#### Accessing app from browser/rest client
```
http://localhost:5050
```

#### Plugins used
- com.github.johnrengelman.shadow
  - Builds shadowjar which happens automatically with gradle build task

## Docker
Created docker image for ratpack app with Alpine base image

#### Building docker image
```
docker build -t saravananperumal/ratpackapp:v1.0 .
```
#### Pushing Docker image to Dockerhub
```
docker push saravananperumal/ratpackapp:v1.0
```
<b>Note:</b> Before running docker push, get registered to Dockerhub and then login to registry using 'docker login' command

### Issues you may come across using Docker in general
<b>Issue:</b> Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?

<b>Solution:</b>

* Check if the docker-machine is up and running
    * Use 'docker-machine ls’ command to list the docker machine instance
* If its available and in Stopped state, then start the machine using the command
    ```
    docker-machine start
    ```
* If its not available, then create a virtual instance for Docker using the command 'docker-machine create --driver virtualbox default’
* Run below command to setup environment for Docker-client
    ```
    'eval "$(docker-machine env default)”'
    ```

<b>Issue:</b> Docker container is running but the hosted app is inaccessible from hosted server

<b>Solution:</b> If your app is working inside of the container when you access it using curl ‘http://localhost:5050'
and not from hosted machine, then you need to check if its a VM which provisions docker to be running on your machine.
If so, you need to get the IP address of docker-machine and then access the app using this IP address and port instead
of trying with localhost or the container IP address.

<b>Issue:</b> Unable to start Gradle daemon due to low memory

<b>Solution:</b> If Jenkins is run from Docker container and is hosted on VirtualBox VM, then you will have to increase
the CPU & Memory for docker-machine instance. You can increase it to 4GB memory and 2 CPU.


## Jenkins Pipeline
Pipeline has been setup to build, unit test, selenium test, code scan with Sonarqube, building docker image,
publish to docker hub, deploy/run image and sends email notification for build status.

## Sonarqube Integration
Integrating Sonarqube can be done using below options,
   - Option 1: Making use of SonarCloud
        - Create an account in https://sonarcloud.io/ (Login using Github Credentials/Create separate account)
        - Create an Organization
        - Add a project to your organization
            - From Github <br/>
                You could add individual repo from your Github Organization for SonarQube scanning or setup for all projects
            - Create Manually <br/>
                Provide below config details to setup manually,
                - Organization - "Provide the Org name created in Step- ii"
                - Project Name - "any name you like"
                - Project Key - "this will be value of groupId.artifactId from your pom.xml"
        - Generating security token while the project is setup
        - Choose the project language and build technology to get the configuration settings specific to your project
        - Copy the configuration settings to your application code and then execute command as described to get your code scanned
   - Option 2: Setting up Sonarqube server
     -  TBD

## Selenium Test Automation
Selenium test has been created to validate UI and for this we created TestApp with HTML page.

- Selenium driver components will be packaged along with your .jar file and so no separate installation is required 
  to run Selenium test
- Chromedriver executable included in the gitrepo should be sufficient and doesn't need Chromdriver to be installed on 
  remote build machine
- To run selenium test you would need Google Chrome browser. So depending on your need, you could install full fledged 
  Chrome browser or headless Chrome browser

Steps to install Chrome headless browser in Ubuntu for Jenkins build,
```
sudo apt-get update
sudo apt-get install -y libappindicator1 fonts-liberation
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome*.deb
```

If you run into issues while installing google-chrome stable version because of dependencies then run the below 
command and then retry,

```
sudo apt-get -f install
```

#### Running Selenium Test
Specific gradle task has been created to run Selenium test
```
gradle seleniumTest
```

## Test App
A simple html page which invokes Web API's using Javascript and displays the response.


## Docker-Compose

Jenkins & Sonarqube will be setup using Docker and its been simplified with docker-compose.

Use below commands to create docker containers 

```
docker-compose -f docker-compose.yml up --build
```

```
docker-compose up -d
```

After Jenkins and Sonarqube has been setup with Docker containers, you should be able to access them from browser. 
If its hosted using docker-machine, then you need to access using its IP Address

<b><u>Jenkins</u></b>

http://localhost:8080

or

http://{DOCKER-ENGINE-IPADDRESS}:8080


<b><u>Sonarqube</u></b>

http://localhost:9000

or

http://{DOCKER-ENGINE-IPADDRESS}:9000

