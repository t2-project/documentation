===================
Energy Measurements
===================

.. admonition:: WIP

   This is currently (beginning of 2024) under work in progress

How does the `T2-Project <https://github.com/t2-project/t2-project>`_ with a microservices architecture compare to the monolithic implementation `T2-Modulith <https://github.com/t2-project/modulith/>`_ in terms of energy consumption?

To answer this question we use different methodologies and tools to measure the energy consumption of both variants under various scenarios.

Results
=======

The results are discussed on the page :doc:`Measurement Results <results>`.

Execution
=========

The files used for executing the measurements are located in the ``energy-tests`` folder of the `DevOps <https://github.com/t2-project/devops>`_ repository.

JMeter
------

Apache JMeter is used to generate requests to the backend with a predefined test plan.
See page :doc:`JMeter <jmeter>` for more information.

Green Metrics Tool
------------------

The Green Metrics Tool is used for measure the energy consumption with different usage case scenarios.
See page :doc:`Green Metrics Tool <gmt>` for more information and our learnings from using it.

Kepler
------

Kepler is used for measure the energy consumption in scenarios with scaling involved.
See page :doc:`Kepler <kepler>` for more information and our learnings from using it.
