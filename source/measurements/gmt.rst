Green Metrics Tool
==================

We are using the `Green Metrics Tool <https://docs.green-coding.berlin/>`_ (GMT) for executing energy tests with different usage scenarios.

The T2 usage scenarios are located in the directory ``energy-tests`` in the GitHub repo `DevOps <https://github.com/t2-project/devops/tree/main/energy-tests/gmt>`_. You can find the documentation about the format ``usage_scenario.yml`` `here <https://docs.green-coding.berlin/docs/measuring/usage-scenario/>`_.

Currently, only usage scenarios are provided that are using `JMeter <https://jmeter.apache.org/>`_ for the execution of some requests to the T2-Project backend:

* Microservices: `UI Backend Service <https://github.com/t2-project/uibackend>`_ → ``uibackend:8080``
* Monolith: `T2-Modulith <https://github.com/t2-project/modulith>`_ → ``backend:8080``

JMeter
------

JMeter uses the test plan ``t2-project-flexible.jmx``.

Example request:

.. code-block:: bash

   jmeter -Jhostname=backend -Jport=8080 -JnumExecutions=1 -JnumUser=1 -JrampUp=0 -JnumProducts=1 -JthinkTimeMin=0 -JthinkTimeAdditionalRange=0 -JtimeBetweenExecutions=0 -JloggingEnabled=true -n -t t2-project-flexible.jmx

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
   * - ``timeBetweenExecutions``
     - time in milliseconds to pause between executions (only make sense in conjunction with ``numExecutions``)
     - no
     - 0
   * - ``loggingEnabled``
     - boolean value, if logging every request is enabled
     - no
     - ``false``


Local testing
-------------

See the `official documentation <https://docs.green-coding.berlin/docs/prologue/introduction/>`_ on how to install and run the Green Metrics Tool on your local system.

The following examples are only meant to check if the usage scenarios are executed without an error. To execute real measurements, see the section 
:ref:`measurement_on_cluster`.

Run with local usage_scenario:

.. code-block:: bash

    python3 runner.py --uri ~/t2-project/devops --filename "energy-tests/gmt/monolith-usage_scenario-minimal-base.yml" --name "T2-Modulith (Minimal Scenario with JMeter)" --skip-system-checks --dev-repeat-run --dry-run --print-logs

Run with remote usage_scenario:

.. code-block:: bash

   python3 runner.py --uri https://github.com/t2-project/devops --branch "main" --filename "energy-tests/gmt/monolith-usage_scenario-minimal-base.yml" --name "T2-Modulith (Minimal Scenario with JMeter)" --skip-system-checks --dev-repeat-run --dry-run --print-logs

.. _measurement_on_cluster:

Measurement on GCB Cluster
--------------------------

To measure a software on the measurement cluster of Green Coding Berlin (GCB) you can submit it via the form on `https://metrics.green-coding.berlin/request.html <https://metrics.green-coding.berlin/request.html>`_.

T2-Modulith (Minimal Scenario with JMeter)

* URL: ``https://github.com/t2-project/devops``
* Filename: ``energy-tests/gmt/monolith-usage_scenario-minimal-base.yml``
* Branch: ``main``
* Hardware: Fujitsu Esprimo P956
* Measurement: One-Off [Free - Fair use]
