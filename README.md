Thermostat Web Gateway Builder Docker image
=============================

This repository contains a Dockerfile for a Thermostat Web Gateway Builder image, which in turn
can be used to build a Thermostat Web Gateway image, call this image `icedtea/thermostat-web-gateway`.

Environment variables
---------------------------------

The icedtea/thermostat-web-gateway image recognizes the following environment
variables that you can set during initialization by passing `-e VAR=VALUE` to
the Docker run command.

|    Variable name              |    Description                              |
| :---------------------------- | -----------------------------------------   |
|  `MONGO_URL`                  | URL for the MongoDB storage instance        |
|  `MONGO_DB`                   | Name of the database to use within the MongoDB storage          |
|  `MONGO_USERNAME`             | Username for the MongoDB database           |
|  `MONGO_PASSWORD`             | Password for the MongoDB database           |
|  `TLS_ENABLED`                | Whether to encrypt communication with the web gateway using TLS (default value: "true") |
|  `WEB_CLIENT_ENABLED`         | Whether to include an endpoint for the Thermostat web client (default value: "true") |
|  `APP_USER`                   | The application user the Java app Thermostat shall monitor runs as (default value: "default") |

Usage
---------------------------------
First, you need to build this image, let's call it `icedtea/thermostat-web-gateway-builder`:

    $ docker build -t icedtea/thermostat-web-gateway-builder .

Next, build a Thermostat Web Gateway version into `icedtea/thermostat-web-gateway` using the builder
image:

    $ s2i build http://icedtea.classpath.org/mirror/git/thermostat-ng-web-gateway icedtea/thermostat-web-gateway-builder icedtea/thermostat-web-gateway

Finally, run the built image while setting the required environment variables:

    $ docker run -e [...] -it icedtea/thermostat-web-gateway
