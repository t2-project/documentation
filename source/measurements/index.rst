
Energy Measurements
===================

How does the `T2-Project <https://github.com/t2-project/t2-project>`_ with a microservices architecture compare to the monolithic implementation `T2-Modulith <https://github.com/t2-project/modulith/>`_ in terms of energy consumption?

To answer this question we use different methodologies and tools to measure the energy consumption of both variants under various scenarios.

The configuration files are located in the ``energy-tests`` folder of the `DevOps <https://github.com/t2-project/devops>`_ repository.

JMeter
------

Apache JMeter is used to generate requests to the backend with a predefined test plan.
See page :doc:`JMeter <jmeter>` for more information.

Green Metrics Tool
------------------

The Green Metrics Tool is used for measure the energy consumption with different usage case scenarios.
See page :doc:`Green Metrics Tool <gmt>` for more information.
