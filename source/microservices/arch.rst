=======================
T2-Project Architecture
=======================

The T2-Project consists of seven services.

.. image:: ../diagrams/microservices-components_total_colour.svg

The green and blue services are the core T2 services. The blue ones participate in the saga, the green ones do not. 
The white things are databases and external services.  

*  `UI <https://github.com/t2-project/ui>`__ : The application frontend.
*  `UIBackend <https://github.com/t2-project/uibackend>`__ : API Gateway for the UI.
*  `Cart <https://github.com/t2-project/cart>`__ : Manages the user shopping carts. It saves the cart contents to the *cart repository*.
*  `Orchestrator <https://github.com/t2-project/orchestrator>`__ : Manages the saga.
*  `Order <https://github.com/t2-project/order>`__ : Persists orders to the *order repository* and marks them as either *success* or *failure*.
*  `Payment <https://github.com/t2-project/payment>`__ : Handles the store’s payment by contacting some credit institute.
*  `Inventory <https://github.com/t2-project/inventory>`__ : Manages the store's products. They are stored in the *product repository*.

The UIBackend communicates over HTTP with a REST like interface.
The Saga participants (marked in blue) use message based communication among each other. 
This is necessary because of the saga pattern. 

The T2-Project realizes the following business process:

.. image:: ../diagrams/microservices-bpmn_sub.png

The activities within the *Saga* subprocess must be executed as a transaction.
The transaction is implemented according to the `Saga Pattern <https://microservices.io/patterns/data/saga.html>`__.

The T2-Project's services realise the activities of the business process like this:

============    ========================================================
Service	        Activity
============    ========================================================
Cart            add item to cart
Inventory       add reservation, delete reservation, commit reservation
Order           create order, reject order
Payment         do payment            
Orchestrator    confirm order
============    ========================================================


Saga
====

The T2-Project's saga is composed of the following steps: 

====  =========  ====================  ========================
Step	Service	  Transaction           Compensation 
====  =========  ====================  ========================
1     Inventory                        cancelReservations()	
2     Order      createOrder()         rejectOrder()
3     Payment    doPayment()           
4     Inventory  commitReservations()  
====  =========  ====================  ========================



The ``doPayment()`` step is the saga's pivot transaction.
If this step succeeds, the saga runs to completion. 

The step ``commitReservations()`` is designed to be repeatable. 
It will succeed eventually. 

The same applies to the compensations ``rejectOrder()`` and ``cancelReservations()``.

Every order is persisted, those that succeeded as well as those that failed.
An order holds, among other details, the order state.
Upon creation the order state is set to *success*. 
As all orders should be persisted, the compensation of creating an order is to set its state to *failed*.
Currently an order cannot be cancelled after submission to the orchestrator. 

The inventory manages the number of available units per product. 
If the inventory decreases the number of available units only after placing the order, the product may not be available anymore because another user bought to many units of that product. 
To prevent such failures the ordered units of a product are locked as soon as they are placed in the shopping cart.
As there is now no action to perform on the inventory before the pivot transaction (``doPayment()``), there is only the compensation that deletes the reservation (in case the saga rolls back) or the step ``commitReservations()`` that handles served reservations. 


Frameworks & Dependencies
=========================

The T2-Project uses the following frameworks (and services):

Spring and Spring Boot
----------------------

=================== ==============
Dependency          Version
=================== ==============
Spring Boot         3.2.x
=================== ==============


Eventuate Tram and Eventuate Tram Saga
--------------------------------------

`Eventuate Tram <https://github.com/eventuate-tram/eventuate-tram-core>`__ is a framework for Transactional Messaging and `Eventuate Tram Sagas <https://github.com/eventuate-tram/eventuate-tram-sagas>`__ is a framework for saga orchestration.
They both work on top of Spring / Spring Boot. 
The T2-Project uses the Eventuate Tram Core framework with Kafka as the message broker and Postgres as the database.

Versions
^^^^^^^^

======================= ==============
Dependency              Version
======================= ==============
io.eventuate.tram.core  0.29.0.RELEASE
io.eventuate.tram.sagas 0.18.0.RELEASE
======================= ==============

Eventuate CDC Service
---------------------

The `Eventuate CDC Service <https://eventuate.io/docs/manual/eventuate-tram/latest/cdc-configuration.html>`__ realizes the `Transactional Outboxing Pattern <https://microservices.io/patterns/data/transactional-outbox.html>`__ required by the Saga Pattern.

Since we are using Postgres, there are two strategies for reading messages/events available to the CDC reader: Postgres WAL and Polling. The default value for polling is 500 milliseconds, which results in a delay of about 3 seconds for the whole Saga operation. Therefore, we switched to Postgres WAL, which is more time efficient and results in a delay of only about 200 milliseconds (without concurrent requests).

================================== ==============
Dependency                         Version
================================== ==============
eventuateio/eventuate-cdc-service  0.16.0.RELEASE
================================== ==============

Message Broker
--------------

The T2-Project uses Kafka and Zookeeper as message broker.

Saga Databases
--------------

The T2-Project uses two PostgreSQL databases for the saga data: one for the inventory service and one for the orchestrator.
The other two services that participate in Saga, Order service and Payment service, don't store their domain data in a relational database. Therefore, they also use the orchestrator's Postgres database for the Saga messages.

The Postgres databases use the container image from `eventuateio <https://hub.docker.com/r/eventuateio/eventuate-postgres>`__ because it already contains the tables required for the transactional outboxing (`source code <https://github.com/eventuate-foundation/eventuate-common/tree/master/postgres>`__).

Domain Databases
----------------

The T2-Project uses MongoDBs and PostgreSQL databases for storing the domain data.
The *cart repository* and the *order repository* are MongoDBs.
The *product repository* used by the Inventory service is a PostgreSQL database.
As mentioned above, the Postgres database of the Inventory service is used for both domain data and saga data to ensure atomicity of local transactions (transactional outbox pattern).


Dependency Management
=====================

`Apache Maven <https://maven.apache.org/>`__ is used for dependency management.

| The microservices are managed as a multi-module project so that the shared dependencies and versions only have to be defined in one central location:
| `microservices/pom.xml <https://github.com/t2-project/microservices/blob/main/pom.xml>`__

Initially, the versions and dependencies of the individual services were managed completely independently of each other in their own *pom.xml*.
However, versions were also managed centrally with the help of environment variables (see the now deleted script `setenv.sh <https://github.com/t2-project/devops/blob/7807b83c69a46085f4a08880e37fd5b9afef5580/setenv.sh>`__).

The structure as a multi-module project offers the following advantages:

* Standard method for managing equal dependencies and versions and for building an entire software system
* Maven automatically ensures the correct build order, which e.g. simplifies the compilation of `common <https://github.com/t2-project/common>`__
* Compared to the initial implementation with environment variables, this simplifies local execution and changing versions
* Less redundant configuration code

However, there are also disadvantages:

* Management of dependencies and versions in a central location contradicts the principle of autonomy of microservices (however, it is possible to overwrite the version definition for individual services if required)
* CI pipeline for building individual services does not start if something is changed in the central `pom.xml <https://github.com/t2-project/microservices/blob/main/pom.xml>`__ (can be solved via a notification mechanism, but has not yet been implemented)


Services
========

All Services are implemented as `Spring Boot <https://spring.io/projects/spring-boot>`__ applications.
This is the services' general package structure:

*  :file:`de.unistuttgart.t2.<service-name>`
*  :file:`de.unistuttgart.t2.<service-name>.saga`
*  :file:`de.unistuttgart.t2.<service-name>.repository`
*  :file:`de.unistuttgart.t2.<service-name>.exception`
*  :file:`de.unistuttgart.t2.<service-name>.domain`

Each service has a subset of those packages, as visualized in the diagram below.
The diagram reads as follows: 
Orchestrator has the *<service-name>* package and a packages *saga*, Order and Inventory have those packages and also a package *repository*, and so on.

.. image:: ../diagrams/microservices-packages.jpg


de.unistuttgart.t2.<service-name>
---------------------------------

The app package contains the following classes, usually prefixed with the service name.
E.g the application class of the Order Service is called *OrderApplication*, the controller is called *OrderController* and so on.

*  Application : annotated with ``@SpringBootApplication``. 
*  Service : contains the logic of the service.
*  Controller : defines the HTTP endpoint of the service. 
   This class is only present, if the service has HTTP endpoints.

Services with complicated configurations have an additional config package that contains the various configuration classes.

de.unistuttgart.t2.<service-name>.saga
------------------------------------------------

The saga package contains classes that are saga specific.
For the participants: 

* CommandHandler : handles incoming messages.

For the orchestrator:

* Saga : definition of the saga.

de.unistuttgart.t2.<service-name>.repository
-------------------------------------------------

The repository packages contain all classes and interfaces for the domain databases.

* Item : the items in the database.
* Repository : an Interface that extends Spring's `MongoRepository <https://docs.spring.io/spring-data/mongodb/docs/current/api/org/springframework/data/mongodb/repository/MongoRepository.html>`__ to access the database.

de.unistuttgart.t2.<service-name>.exceptions
------------------------------------------------------

Any kind of service specific exceptions can be found here.

de.unistuttgart.t2.<service-name>.domain
------------------------------------------

Any classes that represent something domain specific, but does not belong into the repository package. 
Most domain specific things are used by multiple services and thus located in the common package, however things that only one service needs are located here.

Links
=====

For more details on each service, look at the repositories or the API documentation:

*  Order service: `GitHub <https://github.com/t2-project/order>`__
*  Inventory service: `GitHub <https://github.com/t2-project/inventory>`__
*  Payment service: `GitHub <https://github.com/t2-project/payment>`__
*  Orchestrator service: `GitHub <https://github.com/t2-project/orchestrator>`__
*  Cart service: `GitHub <https://github.com/t2-project/cart>`__
*  Credit Institute service: `GitHub <https://github.com/t2-project/creditinstitute>`__
*  UIBackend : `GitHub <https://github.com/t2-project/uibackend>`__
*  UI : `GitHub <https://github.com/t2-project/ui>`__

*  Common: `GitHub <https://github.com/t2-project/common>`__
*  E2E Test: `GitHub <https://github.com/t2-project/e2e-tests>`__

Note: A convenience repo including all microservices exists so that not every repo needs to be downloaded separately: `<https://github.com/t2-project/microservices>`__.
