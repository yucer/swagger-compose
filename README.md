# Unofficial docker compose for swagger images

The aim of this project is to allow the local execution and customization of
swagger services using docker-compose

## Services

So far it allows to run two swagger services in *localhost*:

1. [Swagger online editor](https://github.com/swagger-api/swagger-editor) using its [official docker image](https://hub.docker.com/r/swaggerapi/swagger-editor/)

2. [Swagger online code generator](https://hub.docker.com/r/swaggerapi/swagger-generator/) using its [official doker image](https://github.com/swagger-api/swagger-codegen)

The online editor allows the manual modifications of the specs and also makes direct requests to the online generator.

## Customizing config

But sometimes you want to use another version of the generator or change the its config file. Although some of those options are available in the user interface
of the editor, you can make it persistent modifying the values inside the folder `swagger-editor\config` of this project.

## Use another version of the generator

1. Clone the [swagger-codegen](https://github.com/swagger-api/swagger-codegen) tool

  ```bash
  $ git clone https://github.com/swagger-api/swagger-codegen
  $ cd swagger-codegen
  ```

2. Build the generator:

  ```bash
  $ ./run-in-docker.sh mvn clean
  $ ./run-in-docker.sh mvn package
  ```

3. Build the online-generator:

  ```bash
  $ cd modules/swagger-generator
  $ docker build -t local/swagger-generator .
  ```

  Here you can use your own dockerhub namespace instead of `local`

4. Go to the folder of this project and edit the `docker-compose.yml` file to use:

  ```yaml
  image: local/swagger-generator
  ```

  instead of:

  ```yaml
  image: swaggerapi/swagger-generator
  ```

## Run services

  You can run the services this way:

    ```bash
    $ cd docker-compose
    $ docker-compose up
    ```

  in case of some modification to the config files you might need:

    ```bash
    $ docker-compose down
    $ docker-compose build --no-cache
    $ docker-compose up
    ```
