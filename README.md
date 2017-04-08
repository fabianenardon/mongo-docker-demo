# mongo-docker-demo
A simple demo on how to access mongodb from docker

This sample application shows how to use package a simple MongoDB application with Docker. It highlights also how to do integration tests.

## Running Hadoop and our application:


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

