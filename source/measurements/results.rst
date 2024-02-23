.. _measurement-results:

====================
Measurements Results
====================

This page deals with the measurement related to the main research question:
| Under which scenarios is there a significant difference in energy consumption between the monolith and microservices implementation?

The measurement results listed on this page were generated with the :doc:`Green Metrics Tool <gmt>`. The values relate to the runtime phase, if not mentioned other. While using the Green Metrics Tool, many lessons were learned about what needs to be considered. Please have a look at the section :ref:`GMT Learnings <gmt-learnings>` before looking into the measurement results.

.. contents:: Overview
   :depth: 1
   :local:

Standard Usage Scenario
-----------------------

**Research question:** What is more energy efficient in the standard usage scenario with 1 user, monolith or microservices?

**Scenario:** One user checks out the inventory, thinks for 30 sec, adds a random product to cart, thinks again, add a second product, thinks again, add a third product, and finally confirms the order.

**Findings:**

* The monolith in the standard usage scenario with 1 user is more efficient than the microservices implementation.

.. collapse:: <strong>Measurement</strong>
    :open:

    .. list-table::
      :header-rows: 1
      :stub-columns: 3

      * - Monolith / Microservices
        - Duration [s]
        - Machine Power [W]
        - Machine Energy [J]
        - CPU Energy [J]
        - Memory Energy [J]
        - Network Energy [J]
        - SCI [mgCO2e/order]
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=50008066-07ef-438e-a727-dfcaf1d1c46b>`__
        - 95.72
        - 15.09
        - 1444.10
        - 161.28
        - 46.23
        - 2.47
        - 35.9
      * - `Microservices <https://metrics.green-coding.io/stats.html?id=b3352d36-ba6e-4b9e-9e67-3b5d345a7ff7>`__
        - 106.01
        - 18.05
        - 1913.97
        - 359.95
        - 60.35
        - 18.43
        - 43.9

Multiple executions
-------------------

**Research question:** What is more energy efficient in the simple scenario with 1 user, monolith or microservices?

**Scenario:** One user executes multiple orders one after another.

**Findings:**

* In this basic scenario with 1 user, the microservices system consumes significantly more energy → monolith is more energy-efficient if there is no load
* Some services in the microservices system are always active (Kafka, Zookeeper, Eventuate CDC Service, Orchestrator) that communicate with each other. Therefore in the scenario with 0 executions there is still an energy consumption of 0.46 J due to the network communication.

.. collapse:: <strong>Measurement</strong>
    :open:

    .. list-table::
      :header-rows: 1
      :stub-columns: 3

      * - Monolith / Microservices
        - Number of Executions
        - Think Time [s]
        - Duration [s]
        - Machine Energy [J]
        - CPU Energy [J]
        - Memory Energy [J]
        - Network Energy [J]
        - SCI [mgCO2e/order]
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=f1e0171c-a5f6-4f24-b5e4-558fe334993c>`__
        - 0
        - 0
        - 3.81
        - 113.25
        - 53.19
        - 3.00
        - 0.00
        - N/A
      * - `Microservices <https://metrics.green-coding.io/stats.html?id=e6c84f8f-971e-4401-97b1-3cd75e57c4a9>`__
        - 0
        - 0
        - 4.01
        - 125.64
        - 55.92
        - 3.36
        - 0.46
        - N/A
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=25614e23-d474-4953-a08b-3808f8e46fe6>`__
        - 1
        - 0
        - 5.82
        - 181.52
        - 85.83
        - 5.40
        - 1.02
        - 34.2
      * - `Microservices <https://metrics.green-coding.io/stats.html?id=59ed4330-d15b-465f-933c-9a7d966802f0>`__
        - 1
        - 0
        - 16.56
        - 441.30
        - 164.29
        - 14.00
        - 4.74
        - 87.3
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=7e40ee3b-733e-4b66-aaba-e1e32a412a28>`__
        - 100
        - 0
        - 13.40
        - 393.86
        - 166.47
        - 13.51
        - 83.08
        - 0.8
      * - `Microservices <https://metrics.green-coding.io/stats.html?id=bf22a5c1-670b-4bd2-ba94-ad225cefe7c0>`__
        - 100
        - 0
        - 78.13
        - 1815.27
        - 572.10
        - 67.15
        - 330.28
        - 3.8
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=c8aca13e-428a-4616-8677-93db8ebb0259>`__
        - 100
        - 1
        - 113.50
        - 1809.81
        - 254.30
        - 58.08
        - 84.94
        - 4.4
      * - `Microservices <https://metrics.green-coding.io/stats.html?id=a372a5ed-cb11-45bd-9b4c-8ad626f451bd>`__
        - 100
        - 1
        - 175.16
        - 3457.65
        - 808.74
        - 115.46
        - 345.57
        - 7.6
      
    Number of Executions and the Think Time are pre-configured values.

Load Tests
----------

**Important: The measurements have some problems and have to be fixed**

* a long think time was used, so the average CPU usage in all scenario was quite low
* asynchronous way of the order confirmation in the microservices scenario was not considered
* compute-intensive component was missing

**Research questions:**

* What is more energy efficient in a load test scenario with many parallel users, monolith or microservices?
* How relevant is the CPU, memory and network?

**Scenario:** Many users in parallel: Each user checks out the inventory, think for 30-60 sec, add a random product to cart (3 times) and finally confirms the order. Logging of JMeter requests is disabled.

**Findings:**

* In these scenarios the Microservices system consumes a lot more energy
* Comparison in scenario 100 users:
   - Machine Energy: 2949 J vs. 3891 J (+32 %)
   - CPU Energy: 1050 J vs. 370 J (+184 %)
   - Memory Energy: 95 J vs. 136 J (+43 %) 
   - Network Energy: 311 J vs. 717 J (+131 %)
   - CPU Mean: 7.5 % vs. 27.2 %
   - Memory Mean: 1144 MB vs. 3369 MB
* Conclusion: This comparison is not fair → we need a more compute-intensive scenario

.. collapse:: <strong>Durations</strong>

    .. list-table::
      :header-rows: 1
      :stub-columns: 2
      :align: left

      * - Monolith / Microservices
        - Number of Users
        - Ramp-up time (pre-configured) [s]
        - Duration [s]
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=9c29b4e9-7ee5-416e-9be5-6d183f14e3fc>`__
        - 100
        - 2
        - 186.26
      * - `Microservices <https://metrics.green-coding.io/stats.html?id=ed9b2b05-740e-4769-a533-15e21154dbb0>`__
        - 100
        - 2
        - 185.92
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=2737a2e8-677c-43c0-a167-57f7e9495160>`__
        - 300
        - 5
        - 175.22
      * - `Microservices <https://metrics.green-coding.io/stats.html?id=2c2f7111-9eaf-42be-854a-3ccb71f41241>`__
        - 300
        - 5
        - 182.88

    All measurement runs with monolith system:

    .. list-table::
      :header-rows: 1
      :stub-columns: 2
      :align: left

      * - Monolith
        - Number of Users
        - Ramp-up time (pre-configured) [s]
        - Duration [s]
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=9c29b4e9-7ee5-416e-9be5-6d183f14e3fc>`__
        - 100
        - 2
        - 186.26
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=eb85a781-4e7b-4570-a7bb-b9cd98ab7ebb>`__
        - 200
        - 2
        - 181.97
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=2737a2e8-677c-43c0-a167-57f7e9495160>`__
        - 300
        - 5
        - 175.22
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=1797131a-8bf2-44af-a845-f5fc462e6de0>`__
        - 400
        - 5
        - 180.08
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=d213415f-584c-407e-ab3b-ebc7c911df30>`__
        - 500
        - 5
        - 182.32


.. collapse:: <strong>Energy Consumption</strong>

    .. list-table::
      :header-rows: 1
      :stub-columns: 2
      :align: left

      * - Monolith / Microservices
        - Number of Users
        - Machine Power [W]
        - Machine Energy [J]
        - CPU Energy [J]
        - Memory Energy [J]
        - Network Energy [J]
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=9c29b4e9-7ee5-416e-9be5-6d183f14e3fc>`__
        - 100
        - 15.83
        - 2949.27
        - 370.25
        - 94.94
        - 311.21
      * - `Microservices <https://metrics.green-coding.io/stats.html?id=ed9b2b05-740e-4769-a533-15e21154dbb0>`__
        - 100
        - 20.93
        - 3891.40
        - 1050.28
        - 135.97
        - 717.14
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=2737a2e8-677c-43c0-a167-57f7e9495160>`__
        - 300
        - 17.18
        - 3009.78
        - 513.25
        - 100.76
        - 1608.60
      * - `Microservices <https://metrics.green-coding.io/stats.html?id=2c2f7111-9eaf-42be-854a-3ccb71f41241>`__
        - 300
        - 24.57
        - 4493.86
        - 1525.81
        - 173.44
        - 2402.92

    All measurement runs with monolith system:

    .. list-table::
      :header-rows: 1
      :stub-columns: 2
      :align: left

      * - Monolith
        - Number of Users
        - Machine Power [W]
        - Machine Energy [J]
        - CPU Energy [J]
        - Memory Energy [J]
        - Network Energy [J]
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=9c29b4e9-7ee5-416e-9be5-6d183f14e3fc>`__
        - 100
        - 15.83
        - 2949.27
        - 370.25
        - 94.94
        - 311.21
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=eb85a781-4e7b-4570-a7bb-b9cd98ab7ebb>`__
        - 200
        - 16.42
        - 2990.24
        - 449.09
        - 99.10
        - 844.34
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=2737a2e8-677c-43c0-a167-57f7e9495160>`__
        - 300
        - 17.18
        - 3009.78
        - 513.25
        - 100.76
        - 1608.60
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=1797131a-8bf2-44af-a845-f5fc462e6de0>`__
        - 400
        - 17.66
        - 3180.31
        - 610.23
        - 108.03
        - 2588.05
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=d213415f-584c-407e-ab3b-ebc7c911df30>`__
        - 500
        - 18.43
        - 3360.63
        - 687.72
        - 113.05
        - 3781.67


.. collapse:: <strong>CPU Utilization & Memory Usage</strong>

    Note: JMeter is part of ``system``

    .. list-table::
      :header-rows: 1
      :stub-columns: 1
      :align: left

      * - Monolith / Microservices
        - Number of Users
        - ``system`` CPU Mean [%]
        - ``system`` CPU Max [%]
        - ``system`` Memory Sum Mean [MB]
        - ``system`` Memory Sum Max [MB]
        - ``system`` Memory Sum Min [MB]
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=9c29b4e9-7ee5-416e-9be5-6d183f14e3fc>`__
        - 100
        - 7.52
        - 100.00
        - 1144.43
        - 1199.25
        - 741.55
      * - `Microservices <https://metrics.green-coding.io/stats.html?id=ed9b2b05-740e-4769-a533-15e21154dbb0>`__
        - 100
        - 27.23
        - 100.00
        - 3368.59
        - 3648.12
        - 2708.28
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=2737a2e8-677c-43c0-a167-57f7e9495160>`__
        - 300
        - 14.50
        - 100.00
        - 961.48
        - 1025.16
        - 490.38
      * - `Microservices <?>`__
        - 300
        - 43.17
        - 100.00
        - 3553.26
        - 3829.44
        - 2670.32

    All measurement runs with monolith system:

    .. list-table::
      :header-rows: 1
      :stub-columns: 1
      :align: left

      * - Monolith
        - Number of Users
        - ``system`` CPU Mean [%]
        - ``system`` CPU Max [%]
        - ``system`` Memory Sum Mean [MB]
        - ``system`` Memory Sum Max [MB]
        - ``system`` Memory Sum Min [MB]
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=9c29b4e9-7ee5-416e-9be5-6d183f14e3fc>`__
        - 100
        - 7.52
        - 100.00
        - 1144.43
        - 1199.25
        - 741.55
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=eb85a781-4e7b-4570-a7bb-b9cd98ab7ebb>`__
        - 200
        - 10.83
        - 100.00
        - 956.88
        - 1022.09
        - 505.19
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=2737a2e8-677c-43c0-a167-57f7e9495160>`__
        - 300
        - 14.50
        - 100.00
        - 961.48
        - 1025.16
        - 490.38
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=1797131a-8bf2-44af-a845-f5fc462e6de0>`__
        - 400
        - 17.15
        - 100.00
        - 1041.08
        - 1132.27
        - 536.1
      * - `Monolith <https://metrics.green-coding.io/stats.html?id=d213415f-584c-407e-ab3b-ebc7c911df30>`__
        - 500
        - 19.97
        - 100.00
        - 1104.04
        - 1202.52
        - 507.04
