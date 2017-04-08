# mongo-docker-demo
A simple demo on how to access mongodb from docker

This sample application shows how to use package a simple MongoDB application with Docker. It highlights also how to do integration tests.

## Running MongoDB and the application:


Compile the application and generate the docker images

```
cd sample
mvn clean install -Papp-docker-image
``` 


Start all the services 

```
docker-compose --file docker/docker-compose.yml up -d
```

Run the application
```
docker-compose --file docker/docker-compose.yml run mongo-docker-demo mongo
```

Stop all the services
```
docker-compose --file docker/docker-compose.yml down
``` 

## Running integration tests:

Generates the images
```
mvn clean install -Papp-docker-image
```

Starts mongo service
```
docker-compose --file src/test/resources/docker-compose.yml up -d mongo 
```

Run the application

```
docker-compose --file src/test/resources/docker-compose.yml \
               run mongo-docker-demo \
               java -jar /maven/jar/mongo-docker-demo-1.0-SNAPSHOT-jar-with-dependencies.jar mongo 
```

Run the integration tests

```
docker-compose --file src/test/resources/docker-compose.yml \
               run mongo-docker-demo-tests mvn -f /maven/code/pom.xml \
               -Dmaven.repo.local=/m2/repository -Pintegration-test verify 
```

If you want to remote debug tests, run instead
```
docker run -v ~/.m2/repository:/m2/repository \
       -p 5005:5005 --link mongo:mongo \
       --net resources_default \
       mongo-docker-demo-tests mvn -f /maven/code/pom.xml \
       -Dmaven.repo.local=/m2/repository -Pintegration-test \
       verify -Dmaven.failsafe.debug
```

Stop all the services

```
docker-compose --file src/test/resources/docker-compose.yml down
```

