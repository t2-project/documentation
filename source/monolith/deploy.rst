======================
T2-Modulith Deployment
======================

This section describes different ways to deploy the T2-Modulith.

Deploy on a Kubernetes Cluster
==============================

This section describes how to deploy the T2-Modulith on a Kubernetes cluster. You find the K8s manifest files in the directory :file:`k8s/t2-monolith` in the `DevOps <https://github.com/t2-project/devops>`__ repository.

In the following we explain the basic deployment steps, however, there are also some slightly more sophisticated Bash scripts to make the deployment easier:

* ``start-monolith.sh``
* ``stop-monolith.sh``
* ``update-monolith.sh``

Note: To deploy the T2-Modulith to a managed Kubernetes environment like AWS Elastic Kubernetes Services (EKS), Azure Kubernetes Service (AKS), etc., some additional configuration may be required. Look into the provided Terraform configurations for more information.

Install MongoDB
---------------

The T2-Modulith needs MongoDB. Install it any way you want to, e.g. from helm charts:

.. code-block:: shell

   helm repo add bitnami https://charts.bitnami.com/bitnami
   helm repo update
   helm install mongo --set auth.enabled=false bitnami/mongodb

Deploy PostgreSQL
-----------------

The T2-Modulith needs PostgreSQL. Install it by using the provided YAML file:

.. code-block:: shell

   kubectl apply -f k8s/t2-monolith/base/postgres.yaml

Deploy the backend
------------------

To install the backend use the provided YAML file:

.. code-block:: shell

   kubectl apply -f k8s/t2-monolith/base/backend.yaml

Access the T2-Modulith
----------------------

To access the UI forward the port of the backend to your local machine:

.. code-block:: shell

   kubectl port-forward svc/backend 8081:80

And open `<http://localhost:8081/ui>`__.

You can also access the backend via Swagger-UI: `<http://localhost:8081/swagger-ui/index.html>`__.

Now go to page :doc:`Usage <use>` to figure out what you can do with the T2-Modulith.

Run with Docker
===============

You can run T2-Modulith with all dependencies by using Docker Compose:

.. code-block:: shell

   git clone https://github.com/t2-project/modulith.git
   docker compose up

The container image of the T2-Modulith is stored on `Docker Hub <https://hub.docker.com/r/t2project/modulith>`__.

Now go to page :doc:`Usage <use>` to figure out what you can to with the T2-Modulith application.

Build and Run Locally
=====================

There are different ways on how to build the application on your own and run it locally. 

Build with Maven and run with Docker
------------------------------------

Application gets build by Maven first, then packaged into a Docker image and finally executed.

.. code-block:: shell

   ./mvnw clean install
   docker build -t t2project/modulith:main .
   docker compose up

Build and run with Docker
-------------------------

A multi-stage Dockerfile is used to build the application and place it into a smaller Docker image used for running it.

.. code-block:: shell

   docker build -t t2project/modulith:main -f Dockerfile.full-build .
   docker compose up

Run in development mode
-----------------------

Development mode means that you run the T2-Modulith application on your own, e.g. in debugging mode using your IDE, and only run the dependencies (databases and fake credit institute) with Docker.

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
