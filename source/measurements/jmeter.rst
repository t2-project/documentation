======
JMeter
======

We are using `JMeter <https://jmeter.apache.org/>`_ for generating requests.
JMeter can generate a report with information how much time requests needed, which requests failed, etc. See also the page :doc:`Microservices Usage <../microservices/use>` for how JMeter is used for load generation to trigger SLO violations.

In the context of measuring energy consumption JMeter is used for the execution of a predefined test plan in conjunction with the :doc:`Green Metrics Tool<gmt>`.

Test Plan
=========

We have created one test plan called ``t2-project-flexible.jmx`` that can be used for many different usage case scenarios by configure it via JVM parameters.

**Example request:**

.. code-block:: bash

   jmeter -Jhostname=backend -Jport=8080 -JnumExecutions=1 -JnumUser=1 -JrampUp=0 -JnumProducts=1 -JthinkTimeMin=0 -JthinkTimeAdditionalRange=0 -JpauseBeforeExecution=0 -JpauseAfterExecution=0 -JloggingEnabled=true -n -t t2-project-flexible.jmx

**Parameters:**

.. list-table::
   :header-rows: 1

   * - parameter
     - description
     - required
     - default value
   * - ``hostname``
     - address of the backend
     - yes
     - ``localhost`` / ``backend`` / ``uibackend``
   * - ``port``
     - port of the backend
     - yes
     - ``8081`` (local) / ``8080`` (within Docker network)
   * - ``numExecutions``
     - number of executions (sequential)
     - no
     - 1
   * - ``numUser``
     - number of users (parallel)
     - no
     - 1
   * - ``rampUp``
     - timeout (in seconds) until every user must have been started - one user will be started after every ($rampUp/ $numUser) second(s)
     - no
     - 0
   * - ``numProducts``
     - number of products added to one order
     - no
     - 1
   * - ``thinkTimeMin``
     - minimum amount of time (in milliseconds) a user needs to choose a product
     - no
     - 0
   * - ``thinkTimeAdditionalRange``
     - additional amount of time (in milliseconds) of the normal distribution deciding when the user chooses a product once the timeout is over
     - no
     - 0
   * - ``pauseBeforeExecution``
     - time in milliseconds to pause before an execution - can be useful to delay the start of the first request
     - no
     - 0
   * - ``pauseAfterExecution``
     - time in milliseconds to pause after an execution - can be useful for pauses between multiple executions (``numExecutions``) or to extend the measurement time of the GMT runtime phase (important if there are asynchronous operations happening)
     - no
     - 0
   * - ``loggingEnabled``
     - boolean value, if true for every request and pause a note for GMT will be created
     - no
     - ``false``
   * - ``loggingSCIEnabled``
     - boolean value, if true a `SCI note for GMT <https://docs.green-coding.io/docs/measuring/sci/>`__ will be created right after the request ``POST confirm order`` is sent (``GMT_SCI_R=1``)
     - no
     - ``false``

Local Testing
=============

Configuration
-------------

Add JMeter bin path to your environment variables.

Open ``user.properties`` in the ``bin`` directory and change the value ``overall_granularity`` from 60000 to something smaller:

.. code-block:: ini

   jmeter.reportgenerator.overall_granularity=1000

Simple Execution
----------------

.. code-block:: bash

   jmeter -Jhostname localhost -Jport 8081 -JnumUser 1 -JrampUp 0 -JthinkTimeMin=1000 -JthinkTimeAdditionalRange=0 -JloggingEnabled=true -n -t t2-project-flexible.jmx

Report Generation
-----------------

.. code-block:: bash

   RESULTS_DIR="fixed-single-100-users-30-sec-think-time--modulith-01"
   mkdir $RESULTS_DIR
   jmeter -Jhostname localhost -Jport 8081 -JnumUser 1 -JrampUp 0 -JthinkTimeMin=30000 -JthinkTimeAdditionalRange=30000 -JloggingEnabled=false -n -t t2-project-flexible.jmx -l $RESULTS_DIR/results.csv -e -o $RESULTS_DIR/report
