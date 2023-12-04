.. T2-Project documentation master file, created by
   sphinx-quickstart on Mon May 10 08:39:55 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

========================
T2-Project Documentation
========================

.. toctrees must come first or they won't be displayed correctly

.. toctree::
   :hidden:
   :maxdepth: 1
   :caption: MICROSERVICES

   Overview <microservices/index>
   Architecture <microservices/arch>
   Deployment <microservices/deploy>
   Usage <microservices/use>

.. toctree::
   :hidden:
   :maxdepth: 1
   :caption: MONOLITH

   Overview <monolith/index>
   Architecture <monolith/arch>
   Deployment <monolith/deploy>
   Usage <monolith/use>

.. toctree::
   :maxdepth: 1
   :hidden:
   :caption: MEASUREMENTS

   Overview <measurements/index>
   JMeter <measurements/jmeter>
   Green Metrics Tool <measurements/gmt>

.. toctree::
   :maxdepth: 1
   :hidden:
   :caption: DEVELOPMENT

   Implementation <develop/impl>
   Code Format <develop/format>

Introduction
============

The T2-Project is a reference application provided in two variants:

*  :ref:`Microservices <microservices>` (implementing the Saga pattern)
*  :ref:`Monolith <monolith>` (retaining the modular structure)

The project is loosely based on the `TeaStore Application <https://github.com/DescartesResearch/TeaStore>`__.

| Initially, we only implemented the application in the microservices architecture style and called it **T2-Project**. Later, we added a monolithic variant for comparison.
| The monolith retains the modular structure, therefore we call it **T2-Modulith**.

The initial main purpose of the T2-Project reference application was to trigger SLO violations with regard to response time and availability (see :doc:`Microservices Usage <microservices/use>` for more information).
The initial purpose of the T2-Modulith was to compare a microservices application with a monolith application in terms of energy consumption (see :doc:`Energy Measurements <measurements/index>` for more information).

Repository Structure
====================

The T2-Project is organized under the GitHub organization `t2-project <https://github.com/t2-project>`__ in multiple repositories.

The source code of this documentation is stored in the repository `Documentation <https://github.com/t2-project/documentation>`__.


Monolith implementation
-----------------------

*  `Modulith <https://github.com/t2-project/modulith>`__


Microservices implementation
----------------------------

| A convenience repo including all microservices exists so that not every repo needs to be downloaded separately: `<https://github.com/t2-project/t2-project>`__.

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

This repository contains some DevOps configuration files, e.g. for the deployment of the T2-Project on Kubernetes or Docker:

*  `DevOps <https://github.com/t2-project/devops>`__
