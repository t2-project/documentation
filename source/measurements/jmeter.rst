======
JMeter
======

We are using `JMeter <https://jmeter.apache.org/>`_ for generating load.
JMeter can generate a report with information how much time requests needed, which requests failed, etc. See also the page :doc:`Microservices Usage <../microservices/use>` for how JMeter is used for load generation to trigger SLO violations.

In the context of measuring energy consumption JMeter is only used for the execution of predefined requests.
See the page :doc:`Green Metrics Tool<gmt>` on how JMeter is used in conjunction with the Green Metrics Tool.

Local Usage
===========

Configuration
-------------

Add JMeter bin path to your environment variables.

Open ``user.properties`` in the ``bin`` directory and change the value ``overall_granularity`` from 60000 to something smaller:

.. code-block:: ini

   jmeter.reportgenerator.overall_granularity=1000

Simple execution
----------------

.. code-block:: bash

   jmeter -Jhostname localhost -Jport 8081 -JnumUser 1 -JrampUp 0 -JthinkTimeMin=1000 -JthinkTimeAdditionalRange=0 -JloggingEnabled=true -n -t t2-project-flexible.jmx

Generate report
---------------

.. code-block:: bash

   RESULTS_DIR="fixed-single-100-users-30-sec-think-time--modulith-01"
   mkdir $RESULTS_DIR
   jmeter -Jhostname localhost -Jport 8081 -JnumUser 1 -JrampUp 0 -JthinkTimeMin=30000 -JthinkTimeAdditionalRange=30000 -JloggingEnabled=false -n -t t2-project-flexible.jmx -l $RESULTS_DIR/results.csv -e -o $RESULTS_DIR/report
