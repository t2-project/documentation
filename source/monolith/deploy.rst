======================
T2-Modulith Deployment
======================

This section describes different ways to deploy the T2-Modulith.

Quick start
-----------

You can run T2-Modulith with all dependencies without building anything by using the existing Docker images from `DockerHub <https://hub.docker.com/r/t2project/modulith>`_ and Docker Compose:

.. code-block:: shell

   docker compose up


Build & Run
-----------


There are different ways on how to build and run the application. 

Build with Maven and run with Docker
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Application gets build by Maven first, then packaged into a Docker image and finally executed.

.. code-block:: shell

   ./mvnw clean install -DskipTests
   docker build -t t2project/modulith:main .
   docker compose up

Build and run with Docker
^^^^^^^^^^^^^^^^^^^^^^^^^

A multi-stage Dockerfile is used to build the application and place it into a smaller Docker image used for running it.

.. code-block:: shell

   docker build -t t2project/modulith:main -f Dockerfile.full-build .
   docker compose up

Run in development mode
^^^^^^^^^^^^^^^^^^^^^^^

Development mode means that you run the Modulith application on your own, e.g. in debugging mode using your IDE, and only run the dependencies (databases and fake credit institute) with Docker.

Important: To run the application in development mode, set the Spring profile to ``dev``.

Run dependencies:

.. code-block:: shell

   docker compose -f docker-compose-dev.yml up

If you want to run the application directly from your command line, you can use one of the following commands:


* Spring Boot Maven Plugin (every shell except Powershell):

  .. code-block:: shell

       ./mvnw spring-boot:run -Dspring-boot.run.profiles=dev

* Spring Boot Maven Plugin (Powershell):

  .. code-block:: powershell

       ./mvnw spring-boot:run -D"spring-boot.run.profiles=dev"

* Java:

  .. code-block:: shell

       java -jar target/t2-modulith.war --spring.profiles.active=dev
