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
   :caption: DEVELOPMENT

   develop/format


Introduction
============

The T2-Project is a reference application provided in two variants:

*  :ref:`Microservices <microservices>` (implementing the Saga pattern)
*  :ref:`Modular Monolith <monolith>`

The microservices reference application is loosely based on the `TeaStore Application <https://github.com/DescartesResearch/TeaStore>`__.

Initially, we only implemented the application in the microservices architecture style and called it **T2-Project**. Later, we added a monolithic variant for comparison. The monolith retains the modular structure, therefore we call it **T2-Modulith**.
