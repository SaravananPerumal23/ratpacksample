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

