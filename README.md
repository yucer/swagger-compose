# Unofficial docker compose for swagger images

The aim of this project is to allow the local execution and customization of
swagger services using docker-compose

## Services

So far it allows to run two swagger services in *localhost*:

1. [Swagger online editor](https://github.com/swagger-api/swagger-editor) using its [official docker image](https://hub.docker.com/r/swaggerapi/swagger-editor/)

2. [Swagger online code generator](https://hub.docker.com/r/swaggerapi/swagger-generator/) using its [official doker image](https://github.com/swagger-api/swagger-codegen)

The online editor allows the manual modifications of the specs and also makes direct requests to the online generator.

## Local generation

But if the generation must be local, because of privacy restrictions you can...

## Run services

  You can run the services this way:

    ```bash
    docker-compose up
    ```

  in case of some modification to the config files you might need:

    ```bash
    docker-compose down
    docker-compose build
    docker-compose up
    ```

## If you want to locally build the code generator image

1. Clone the [swagger-codegen](https://github.com/swagger-api/swagger-codegen) tool

  ```bash
  git clone https://github.com/swagger-api/swagger-codegen
  cd swagger-codegen
  ```

2. Build the generator:

  ```bash
  ./run-in-docker.sh mvn clean
  ./run-in-docker.sh mvn package
  ```

3. Build the online-generator:

  ```bash
  cd modules/swagger-generator
  docker build -t swaggerapi/swagger-generator .
  ```
