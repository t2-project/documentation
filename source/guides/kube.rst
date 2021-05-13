.. _usage:

Run on a Kubernetes Cluster
========================================

The preferred deployment for the T2 Store is in a Kubernetes cluster (with at least 2 nodes).

.. code-block:: php

   wget <all-in-one-deployment>
   kubectl create -f .


Run Locally  
===========

You can run the entire T2 Store locally, either by using the pre build docker images, or by building all services yourself. 

The following guide describes how to build an run the T2 services with the Order service as an example. 
You can build all other services (with minor exceptions) the same way.
You just need to replace 'order' with the respective service name.

Step 0 : Clone Repository
----------------------------------------------------

.. code-block:: php

   git clone https://github.com:t2-project/order.git


Step 1 : Versions and Environment Variables
----------------------------------------------------

The T2 Store is build with the following dependencies and tools. 
There is no guarantee that it works with others as well. 

======================= ==========================
Name                    Version
======================= ==========================
Maven                   :file:`3.6.3`
Spring Boot             :file:`2.4.4`
io.eventuate.tram.core  :file:`0.29.0.RELEASE`
io.eventuate.tram.sagas :file:`0.18.0.RELEASE`
jaeger                  :file:`  `
prometheus              :file:`  `
resilience4j            :file:`  `
junit4                  :file:`  `
Docker                  :file:`20.10.6`
======================= ==========================

The :file:`pom.xml` files read the versions from environment variables. 
That means you either have to manually export the versions you want to use, or you source the provided `setenv.sh <https://github.com/t2-project/kube/blob/main/setenv.sh>`__ file.

.. code-block:: php

   wget https://raw.githubusercontent.com/t2-project/kube/main/setenv.sh
   . ./setenv.sh


Step 2 : Set Application properties
----------------------------------------

Set the `application properties <https://github.com/t2-project/order/tree/main/src/main/resources>`__.
They are in located at :file:`./src/main/resources/`
You want to consult the service's README on the meaning of the properties.

Step 3 : Build Local Dependencies
------------------------------------------

Most services of the T2 store depend on `common <https://github.com/t2-project/common>`__, thus you need to build that first:

.. code-block:: php

   git clone https://github.com/t2-project/common.git
   cd common/
   mvn clean install

And install it to your local maven repository:  

.. code-block:: php

   mvn install:install-file -Dfile=./target/common-1.0-SNAPSHOT.jar  -DpomFile=./pom.xml

Step 2.1 : Exceptions for Service E2E Test
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The E2E Test also depends on the saga participants *inventory*, *payment* and *order*.

You must build and install them to your local maven repository as well.

.. code-block:: php

   git clone https://github.com/t2-project/payment.git
   cd payment/
   mvn clean install
   mvn install:install-file -Dfile=./target/payment-0.0.1-SNAPSHOT.jar.original -DpomFile=./pom.xml
   
.. code-block:: php

   git clone https://github.com/t2-project/inventory.git
   cd inventory/
   mvn clean install
   mvn install:install-file -Dfile=./target/inventory-0.0.1-SNAPSHOT.jar.original -DpomFile=./pom.xml

.. code-block:: php

   git clone https://github.com/t2-project/order.git
   cd order/
   mvn clean install
   mvn install:install-file -Dfile=./target/order-0.0.1-SNAPSHOT.jar.original -DpomFile=./pom.xml


Step 4 : Build and Run
----------------------

Now you can build and run the order service.

.. code-block:: php

   cd order/
   ./mvnw spring-boot:run

Or like this, in case you want to supply specific application properties (remember to use the path to *your* properties file).

.. code-block:: php

   cd order/
   mvn clean install
   java -jar -Dspring.config.location=./src/main/resources/application.local.properties ./target/order-0.0.1-SNAPSHOT.jar

Step 5 : Build Docker Image
---------------------------

Each service repository contains a Dockerfile to build an image of that service.



Load Generation
===============

You can generate load manually by sending requests to the UIBackend (or using the UI, once it is there).
Confer the `UI Backend's README <https://github.com/t2-project/uibackend>`__ on how to talk to the UI Backend.

Or you can use a Load Generator to send request.
I recommend `Apache JMeter <https://jmeter.apache.org/>`__.

Apache JMeter
-------------

To run the T2 Store with the JMeter Load Generator, you must do the following :

#. Deploy the T2 Store
#. Install JMeter
#. Create or download a load profile
#. Run the load generator

Confer the `TeaStore Wiki <https://github.com/DescartesResearch/TeaStore/wiki/Testing-and-Benchmarking#22-jmeter>`__ on how to install and use JMeter.
Just use the T2 Store load profiles instead of those from the TeaStore. 

You can download the T2 Store load profiles here : `<https://github.com/t2-project/kube/tree/main/loadprofiles>`__

Random Infinite Load Profile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The profile :file:`t2-store-random_infinite.jmx` generates requests to the UI Backend as visualized below.
Beware to set :file:`-Jhostname` and :file:`-Jport` to your UI Backend's address and port. 

.. image:: ../arch/figs/load_generator.jpg

With this profile the generator adds between 1 to 5 products to the cart, and confirm the order afterwards.
It chooses the product at random from the products in the inventory.


Fixed Single Load Profile
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The profile :file:`t2-store-fixed_single.jmx` is similar to the previous one, but, as visualized below, it places only one order over 3 random products.

.. image:: ../arch/figs/load_generator_single.jpg

prometheus
==========

The T2 store can be monitored with `Prometheus <https://prometheus.io/>`__

These services expose metric with help of `Micrometer <https://TODO>`__

*  `Credit Institute Service <svc-creditinstitute>`
*  usw.


Rules and Alerts
----------------

may be found here `TODO insert link to file <https://github.com/t2-project/TODO>`__

They are for the Credit Institute and represent the following SLO:

Response Time
^^^^^^^^^^^^^
TODO

Availability
^^^^^^^^^^^^
TODO


jaeger / opentracing
====================

The T2 store can be traced with `Jaeger <https://www.jaegertracing.io/>`__

The service use `Maven link??  <https://TODO>`__ to enable tracing. 
the send spans to jaeger service as set in application properties