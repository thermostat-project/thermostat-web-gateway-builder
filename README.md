Thermostat Web Gateway Builder (32-bit) Docker image
=============================

This repository contains a Dockerfile for a Thermostat Web Gateway Builder image, which in turn
can be used to build a Thermostat Web Gateway image, call this image `icedtea/thermostat-web-gateway-32bit`.
This image builds and runs using a 32-bit JVM.

Environment variables
---------------------------------

The icedtea/thermostat-web-gateway-32bit image recognizes the following environment
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
|  `BASIC_AUTH_CONFIG`          | Path to configuration file for Basic authentication |
|  `APP_USER`                   | The application user the Java app Thermostat shall monitor runs as (default value: "default") |

Usage
---------------------------------
First, you need to build this image, let's call it `icedtea/thermostat-web-gateway-32bit-builder`:

    $ docker build -t icedtea/thermostat-web-gateway-32bit-builder .

Next, build a Thermostat Web Gateway version into `icedtea/thermostat-web-gateway-32bit` using the builder
image:

    $ s2i build http://icedtea.classpath.org/mirror/git/thermostat-ng-web-gateway icedtea/thermostat-web-gateway-32bit-builder icedtea/thermostat-web-gateway-32bit

Finally, run the built image while setting the required environment variables:

    $ docker run -e [...] -it icedtea/thermostat-web-gateway-32bit

To include a custom configuration file, such as for Basic authentication configuration, you can include it as a volume when running the built image:

    $ docker run -e BASIC_AUTH_CONFIG=/container/path/basic-config.properties -v /local/path/basic-config.properties:/container/path/basic-config.properties:ro,Z [...]
