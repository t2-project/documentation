.. T2-Project documentation master file, created by
   sphinx-quickstart on Mon May 10 08:39:55 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

========================
T2-Project Documentation
========================

.. toctrees must come first or they won't be displayed correctly

.. toctree::
   :caption: MICROSERVICES
   :maxdepth: 2
   :hidden:

   Overview <microservices/index>
   Architecture <microservices/arch>
   Deployment <microservices/deploy>
   Usage <microservices/use>

.. toctree::
   :caption: MODULITH
   :maxdepth: 2
   :hidden:

   Overview <modulith/index>
   Architecture <modulith/arch>
   Deployment <modulith/deploy>
   Usage <modulith/use>

.. toctree::
   :caption: MEASUREMENTS
   :maxdepth: 2
   :hidden:

   Overview <measurements/index>
   JMeter <measurements/jmeter>
   Green Metrics Tool <measurements/gmt>
   Kepler <measurements/kepler>
   Results <measurements/results>

.. toctree::
   :caption: DEVELOPMENT
   :maxdepth: 2
   :hidden:

   Implementation <develop/impl>
   Code Format <develop/format>

Introduction
============

The T2-Project is a reference application provided in two variants:

*  :ref:`T2-Microservices <microservices>` (implementing the saga pattern)
*  :ref:`T2-Modulith <modulith>` (monolith with the same modular structure)

The project is loosely based on the `TeaStore Application <https://github.com/DescartesResearch/TeaStore>`__.

| Initially, we only implemented the application in the microservices architecture style and called it *T2-Project*. Later, we added a monolithic variant for comparison.
| The monolith retains the modular structure, therefore we call it **T2-Modulith**.
| In order to distinguish the individual variants and the overall project linguistically, we now use the term **T2-Project** to refer to the overall project, including both variants, and call the initial microservices implementation **T2-Microservices**.

The initial main purpose of the T2-Project reference application was to trigger SLO violations with regard to response time and availability (see :doc:`Microservices Usage <microservices/use>` for more information).
The purpose of the T2-Modulith is to compare a microservices application with a modulith application, mainly in regards of energy efficiency (see :doc:`Energy Measurements <measurements/index>` for more information).

Source Code
===========

The T2-Project is organized under the GitHub organization `t2-project <https://github.com/t2-project>`__ in multiple repositories.

A convenience repo including all repositories exists so that not every repo needs to be cloned separately: `<https://github.com/t2-project/t2-project>`__.

The source code of this documentation is stored in the repository `Documentation <https://github.com/t2-project/documentation>`__.

Common deployment and configuration files, e.g. for Kubernetes or Docker, are located in one repository called `DevOps <https://github.com/t2-project/devops>`__.

Modulith implementation
-----------------------

*  `Modulith <https://github.com/t2-project/modulith>`__

Microservices implementation
----------------------------

| A convenience repo including all microservices exists so that not every repo needs to be downloaded separately: `<https://github.com/t2-project/microservices>`__.

Shared domain classes are part of the `Common <https://github.com/t2-project/common>`__ repository, that is a dependency of all services.

Core services:

*  `Order service <https://github.com/t2-project/order>`__
*  `Inventory service <https://github.com/t2-project/inventory>`__
*  `Payment service <https://github.com/t2-project/payment>`__
*  `Orchestrator service  <https://github.com/t2-project/orchestrator>`__
*  `Cart service  <https://github.com/t2-project/cart>`__
*  `UIBackend service <https://github.com/t2-project/uibackend>`__
*  `UI <https://github.com/t2-project/ui>`__

Supplemental services:

*  `E2E Test <https://github.com/t2-project/e2e-tests>`__
*  `Credit Institute service  <https://github.com/t2-project/creditinstitute>`__
