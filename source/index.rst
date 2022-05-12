.. T2 Store documentation master file, created by
   sphinx-quickstart on Mon May 10 08:39:55 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

======================
T2 Store Documentation
======================

.. toctrees must come first or they won't be displayed correctly

.. toctree::
   :hidden:
   :maxdepth: 1
   :caption: ARCHITECTURE

   arch/arch 


.. toctree::
   :maxdepth: 2
   :hidden:
   :caption: HOWTOS

   guides/deploy
   guides/use

.. toctree::
   :maxdepth: 1
   :hidden:
   :caption: JAVADOC

   javadoc/common/packages
   javadoc/order/packages
   javadoc/payment/packages
   javadoc/inventory/packages
   javadoc/orchestrator/packages
   javadoc/uibackend/packages
   javadoc/ui/packages
   javadoc/cart/packages
   javadoc/creditinstitute/packages
   javadoc/e2etest/packages


Introduction
============

The T2 Store is a micro-service reference application that implements the Saga pattern.
It is loosely based on the `TeaStore Application <https://github.com/DescartesResearch/TeaStore>`__.

The T2 Store consists of seven services that realise the store’s business logic plus two additional services, one to simulate an external payment provider, as an example some credit institute and the other to test the store at runtime. 

All services are Spring Boot Applications. 
They are instrumented with `Prometheus <https://prometheus.io/>`__ for metrics and with `Jaeger <https://www.jaegertracing.io/>`__  for tracing.

See the :ref:`architecture overview <arch>` for more information about the architecture.
See the :ref:`howtos  <use>` and :ref:`howtos  <deploy>` for more information about how to use the store.


.. Requirements
.. ------------

.. The T2 Store is developed as a reference application.

.. TODO : copy Requirements from proposal

Repository Structure
--------------------

.. TODO : where do i want do put this?

The T2 Store services are organized in multiple repositories under the `t2-project <https://github.com/t2-project>`__ GitHub organization.

These repositories contain the core services of the T2 Store:

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

This repository contains the files for deploying the T2 store on kubernetes as well other files, that did not belong anywhere else:

*  `Kube <https://github.com/t2-project/kube>`__


.. Common Repository Structure
.. ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
.. 
.. Each service repositories contain the following files and directories:
.. 
.. *  Dockerfile : To build a docker image of the service.
.. *  README.md : The readme. Look here for more information about the service.
.. *  src/ : Actual code of the service.



.. Indices and tables
.. ------------------
.. 
.. * :ref:`genindex`
.. * :ref:`modindex`
.. * :ref:`search`
