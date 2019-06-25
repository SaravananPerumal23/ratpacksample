# ratpacksample
Sample Ratpack app


## Building project
./gradlew build

## Running project
./gradlew run

(or)

java -jar my.ratpackapp-1.0-SNAPSHOT-all.jar

## Building docker image
docker build -t saravananperumal/ratpackapp:v1.0 .

## Pushing Docker image to Dockerhub
docker push saravananperumal/ratpackapp:v1.0

Note: Before running docker push, get registered to Dockerhub and then login to registry using 'docker login' command

## Plugins
- com.github.johnrengelman.shadow
  - Builds shadowjar which happens automatically with gradle build task



## Jenkins Pipeline


## SonarQube Integration
    Integrating Sonarqube can be done using 2 options,
    1. Making use of SonarCloud
    2. Setting up SonarQube in premises

### 1. Making use of SonarCloud

Note: Most of the steps mentioned below are at high level and as you get into this SonarCloud you should be able to play around.
        i. Create an account in https://sonarcloud.io/ (Login using Github Credentials/Create separate account)
        ii. Create an Organization
        iii. Add a project to your organization
            a. From Github
                You could add individual repo from your Github Organization for SonarQube scanning or setup for all projects
            b. Create Manually
                Organization — <Provide the Org name created in Step- ii >
                Project Name — < any name you like>
                Project Key- < this will be value of groupId.artifactId from your pom.xml >
        iv. Generating security token while the project is setup
        v. Choose the project language and build technology to get the configuration settings specific to your project
        vi. Copy the configuration settings to your application code and then execute command as described to get your code scanned

### Option - 2
    Installing SonarQube locally