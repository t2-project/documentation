.. _microservices:

========================
T2-Project Microservices
========================

The T2-Project consists of seven services that realize the store’s business logic plus two additional services, one to simulate an external payment provider, as an example some credit institute and the other to test the store at runtime. 

All services are Spring Boot Applications. 
They are instrumented with `Prometheus <https://prometheus.io/>`__ for metrics and with `Jaeger <https://www.jaegertracing.io/>`__  for tracing.

See page :doc:`Architecture <arch>` for more information about the microservices architecture.
See pages :doc:`Usage <use>` and :doc:`Deployment <deploy>` for more information about how to use the T2-Project.


.. Requirements
.. ------------

.. The T2-Project is developed as a reference application.

.. TODO : copy Requirements from proposal


Repository Structure
--------------------

| The T2-Project services are organized in multiple repositories under the `t2-project <https://github.com/t2-project>`__ GitHub organization.
| A convenience repo also exists so that not every repo needs to be downloaded separately: `<https://github.com/t2-project/t2store>`__.

These repositories contain the core services of the T2-Project:

*  `Order service <https://github.com/t2-project/order>`__
*  `Inventory service <https://github.com/t2-project/inventory>`__
*  `Payment service <https://github.com/t2-project/payment>`__
*  `Orchestrator service  <https://github.com/t2-project/orchestrator>`__
*  `Cart service  <https://github.com/t2-project/cart>`__
*  `UIBackend service <https://github.com/t2-project/uibackend>`__
*  `UI <https://github.com/t2-project/ui>`__

These repositories contain the supplemental services:

*  `E2E Test <https://github.com/t2-project/e2e-test>`__
*  `Credit Institute service  <https://github.com/t2-project/creditinstitute>`__

This repository contains shared domain classes. 
It is a dependency to all other services:

*  `Common <https://github.com/t2-project/common>`__

This repository contains the source for this documentation:

*  `Documentation <https://github.com/t2-project/documentation>`__

This repository contains the files for deploying the T2-Project on kubernetes as well other files, that did not belong anywhere else:

*  `Kube <https://github.com/t2-project/kube>`__


.. Common Repository Structure
.. ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. 
.. Each service repositories contain the following files and directories:
.. 
.. *  Dockerfile : To build a docker image of the service.
.. *  README.md : The readme. Look here for more information about the service.
.. *  src/ : Actual code of the service.
