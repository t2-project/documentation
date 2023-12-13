==================
Green Metrics Tool
==================

We are using the `Green Metrics Tool <https://docs.green-coding.berlin/>`_ (GMT) for executing energy tests with different usage scenarios.

The T2 usage scenarios are located in the directory ``energy-tests`` in the GitHub repo `DevOps <https://github.com/t2-project/devops/tree/main/energy-tests/gmt>`_. You can find the documentation about the format ``usage_scenario.yml`` `here <https://docs.green-coding.berlin/docs/measuring/usage-scenario/>`_.

Currently, only usage scenarios are provided that use :doc:`JMeter <jmeter>` for the execution of requests to the T2-Project backend:

* Microservices: `UI Backend Service <https://github.com/t2-project/uibackend>`_ → ``uibackend:8080``
* Monolith: `T2-Modulith <https://github.com/t2-project/modulith>`_ → ``backend:8080``

Local testing
=============

See the `official documentation <https://docs.green-coding.berlin>`_ on how to install and run the Green Metrics Tool on your local system.

The following examples are only meant to check if the usage scenarios are executed without an error. To execute real measurements, see the section :ref:`measurement_on_cluster`.

Run with local usage_scenario.yml:

.. code-block:: bash

    python3 runner.py --uri ~/t2-project/devops --filename "energy-tests/gmt/monolith-usage_scenario-minimal-base.yml" --name "T2-Modulith (Minimal Scenario with JMeter)" --skip-system-checks --dev-repeat-run --dry-run --print-logs

Run with remote usage_scenario.yml:

.. code-block:: bash

   python3 runner.py --uri https://github.com/t2-project/devops --branch "main" --filename "energy-tests/gmt/monolith-usage_scenario-minimal-base.yml" --name "T2-Modulith (Minimal Scenario with JMeter)" --skip-system-checks --dev-repeat-run --dry-run --print-logs

The parameters ``--skip-system-checks``, ``--dev-repeat-run``, ``--dry-run`` and ``--print-logs`` are all optional. The first three are used to speed up the execution of usage scenarios for testing.
Depending on the usage scenario you may need to remove the parameter ``--dry-run``. ``--dry-run`` skips all sleeps that may be required to execute a usage scenario e.g. to wait for all services to be ready.

.. _measurement_on_cluster:

Measurement on GCB Cluster
==========================

To measure a software on the `measurement cluster provided by Green Coding Berlin (GCB) <https://docs.green-coding.berlin/docs/measuring/measurement-cluster/>`_ you can submit it via the form on `https://metrics.green-coding.berlin/request.html <https://metrics.green-coding.berlin/request.html>`_.

Example form inputs:

* Name: T2-Modulith (Minimal Scenario with JMeter)
* URL: ``https://github.com/t2-project/devops``
* Filename: ``energy-tests/gmt/monolith-usage_scenario-minimal-base.yml``
* Branch: ``main``
* Hardware: Fujitsu Esprimo P956
* Measurement: One-Off [Free - Fair use]

Results
-------

All executed measurements can be found on the GMT page `Repository overview <https://metrics.green-coding.berlin/repositories.html>`_ under the repository ``/t2-project/devops``. There you also have the possibility to compare multiple measurements on your own:

* Open the repository ``/t2-project/devops``
* Select the measurements you want to compare
* Click the button "Compare: x Run(s)" on the top of the page

The results are discussed on the page :doc:`Measurement Results <results>`.
