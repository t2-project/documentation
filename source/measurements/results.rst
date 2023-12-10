===================
Measurement Results
===================

The measurement results listed on this page were generated with the :doc:`Green Metrics Tool <gmt>`. The values relate to the runtime phase, if not mentioned other.

.. contents:: Overview
   :depth: 2
   :local:

Modulith 
========

In this section the findings of executing different usage scenarios with the monolith application are discussed.

Idle
----

**Research question:** How much energy is consumed on the test machine if the target application has nothing to do?

**Scenario:** JMeter starts with the usual test plan, but no requests are made

.. list-table::
   :header-rows: 1
   :stub-columns: 1

   * - Number of executions
     - Duration [s]
     - Machine Energy [J]
     - CPU Energy [J]
     - Memory Energy [J]
     - Network Energy [J]
   * - `0 <https://metrics.green-coding.berlin/stats.html?id=f1e0171c-a5f6-4f24-b5e4-558fe334993c>`__
     - 3.81
     - 113.25
     - 53.19
     - 3.00
     - 0.00

**Findings:**

* JMeter itself already consumes a lot of energy when it starts executing a test plan, even no requests are made. However, this only effects the beginning of the phase and should not influence the behavior of the backend later on. Also, because we use JMeter in all measurements with the same test plan, comparisons should also not be a problem.
* Machine components other than CPU and memory also consume a significant amount of energy. In the scenario circa 60 J.

Logging on/off
--------------

**Research question:** How much is the impact of JMeter logging on the energy consumption?

**Scenario:** One user executes 100 orders one after another.

.. list-table::
   :header-rows: 1
   :stub-columns: 1

   * - Logging
     - Duration [s]
     - Machine Energy [J]
     - CPU Energy [J]
     - Memory Energy [J]
     - Network Energy [J]
   * - `on <https://metrics.green-coding.berlin/stats.html?id=7e40ee3b-733e-4b66-aaba-e1e32a412a28>`__
     - 13.40
     - 393.86
     - 166.47
     - 13.51
     - 83.08
   * - `off <https://metrics.green-coding.berlin/stats.html?id=940a3183-0724-46c4-89ab-d52923dbe98f>`__
     - 11.93
     - 346.74
     - 144.05
     - 12.20
     - 83.06

**Findings:**

* Logging of all requests requires a significant amount of energy (in this scenario +13%)

Multiple executions
-------------------

*Here we are using some scenarios consisting of only one GMT flow and some consisting of multiple GMT flows. Multiple flows means that we get results in a more fine-grained way for every individual flow.*

**Research questions:**

* Should the first measurements be ignored, because the JVM needs some time to get warm?
* Is the energy consumption proportional to the number of executions?

One GMT flow
~~~~~~~~~~~~

**Scenario:** One user executes multiple orders one after another.

.. list-table::
   :header-rows: 1
   :stub-columns: 1

   * - Number of Executions
     - Duration [s]
     - Machine Energy [J]
     - CPU Energy [J]
     - Memory Energy [J]
     - Network Energy [J]
     - SCI [mgCO2e/order]
   * - `0 <https://metrics.green-coding.berlin/stats.html?id=f1e0171c-a5f6-4f24-b5e4-558fe334993c>`__
     - 3.81
     - 113.25
     - 53.19
     - 3.00
     - 0.00
     - N/A
   * - `1 <https://metrics.green-coding.berlin/stats.html?id=25614e23-d474-4953-a08b-3808f8e46fe6>`__
     - 5.82
     - 181.52
     - 85.83
     - 5.40
     - 1.02
     - 34.2
   * - `2 <https://metrics.green-coding.berlin/stats.html?id=a75a499b-b066-440c-ba0d-9ac8c552baa4>`__
     - 5.98
     - 184.07
     - 87.43
     - 5.46
     - 1.93
     - 17.4
   * - `100 <https://metrics.green-coding.berlin/stats.html?id=7e40ee3b-733e-4b66-aaba-e1e32a412a28>`__
     - 13.40
     - 393.86
     - 166.47
     - 13.51
     - 83.08
     - 0.8

**Findings:**

* calculations:
   - required energy for the second execution (based on the difference between 1 and 2 executions):
      + Duration: 0.16 s
      + Machine Energy: 2.55 J
      + CPU Energy 1.6 J
      + Memory Energy: 0.04 J
      + Network Energy: 0.91 J
   - average required energy for one execution in the scenario with 100 executions (consumption of 0 executions is subtracted):
      + Duration: 0.1 s
      + Machine Energy: 2.81 J
      + CPU Energy 1.13 J
      + Memory Energy: 0.11 J
      + Network Energy: 0.83 J
* CPU energy consumption gets more efficient with more executions

Multiple GMT flows - single user
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Scenario:** `25 flows á 100 executions <https://metrics.green-coding.berlin/stats.html?id=b5478c99-c8b4-4f65-a25b-99180f5ced2f>`__

.. list-table::
   :header-rows: 1
   :stub-columns: 1

   * - Flow
     - Duration [s]
     - Machine Power [W]
     - Machine Energy [J]
     - Network Energy [J]
     - ``backend`` CPU Utilization Mean [%]
   * - All
     - 226.04
     - 24.28
     - 5488.78
     - 2079.65
     - 10.33
   * - 1.
     - 12.10
     - 26.93
     - 325.9
     - 83.52
     - 29.38
   * - 2.
     - 8.94
     - 27.96
     - 249.82
     - 83.14
     - 23.90
   * - 3.
     - 9.32
     - 24.82
     - 231.35
     - 83.12
     - 13.57
   * - 4.
     - 8.85
     - 24.54
     - 217.22
     - 83.12
     - 11.43
   * - 5.
     - 8.55
     - 25.52
     - 218.25
     - 83.12
     - 13.22
   * - 6.
     - 8.92
     - 24.00
     - 214.04
     - 83.15
     - 9.95
   * - 7.
     - 8.55
     - 25.10
     -  214.54
     - 83.14
     - 10.69
   * - 8.
     - 8.80
     - 24.28
     - 213.72
     - 83.15
     - 9.85
   * - ...
     - 
     - 
     - 
     - 
     - 
   * - 16.
     - 9.30
     - 23.24
     - 216.14
     - 83.15
     - 5.76
   * - 17.
     - 8.90
     - 25.48
     - 208.98
     - 83.13
     - 6.85
   * - 18.
     - 8.69
     - 24.45
     - 212.39
     - 83.16
     - 9.57
   * - 19.
     - 8.75
     - 24.06
     - 210.50
     - 83.17
     - 7.81
   * - 20.
     - 8.95
     - 23.54
     - 210.67
     - 83.13
     - 6.71
   * - 21.
     - 9.04
     - 22.98
     - 207.64
     - 83.16
     - 4.99
   * - 22.
     - 9.01
     - 23.00
     - 207.34
     - 83.17
     - 6.53
   * - 23.
     - 8.97
     - 23.62
     - 211.96
     - 83.15
     - 6.50
   * - 24.
     - 9.02
     - 23.65
     - 213.38
     - 83.16
     - 7.29
   * - 25.
     - 8.82
     - 23.46
     - 206.83
     - 83.16
     - 7.37

**Findings:**

* Using multiple flows has the disadvantage, that JMeter has a bigger impact. Therefore the energy values are not a good metric here for comparison. Instead we are using the CPU utilization of ``backend`` here for comparison.
* The average CPU utilization of the first (29.38 %) and the second flow (23.90 %) with 100 executions each is much higher than the subsequent flows (<14 %)
* After the 10. flow the average CPU utilization stays under 10 %
* There is some kind of optimizations happening!

Multiple GMT flows - 100 parallel users
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

**Scenario:** `10 flows á 100 users <https://metrics.green-coding.berlin/stats.html?id=fc9d3906-c0fa-4327-85d6-eac12b4a72ed>`__

.. list-table::
   :header-rows: 1
   :stub-columns: 1

   * - Flow
     - Duration [s]
     - Machine Power [W]
     - Machine Energy [J]
     - Network Energy [J]
     - ``backend`` CPU Utilization Mean [%]
   * - All
     - 79.11
     - 28.48
     - 2253.41
     - 951.19
     - 19.79
   * - 1.
     - 27.36
     - 23.28
     - 637.00
     - 130.40
     - 18.22
   * - 2.
     - 6.03
     - 30.46
     - 183.77
     - 95.65
     - 22.15
   * - 3.
     - 6.02
     - 32.00
     - 192.67
     - 94.39
     - 20.26
   * - 4.
     - 5.76
     - 31.15
     - 179.58
     - 92.58
     - 21.17
   * - ...
     - 
     - 
     - 
     - 
     - 
   * - 9.
     - 5.64
     - 31.16
     - 175.69
     - 89.25
     - 19.43
   * - 10.
     - 5.57
     - 30.30
     - 168.87
     - 88.02
     - 17.71

**Findings:**

* The first flow required a lot of time (reason unknown) and therefore also a lot more energy.
* All the other results were quite similar with a little increase in performance and a little decrease in energy consumption.

**What does the findings mean for other tests?**

* It makes sense to execute multiple flows to be able to only use representative results and ignore the first ones

Think time
----------

**Research question:** How does the think time effect the result?

**Scenario:** One user executes one order with different think times.

.. list-table::
   :header-rows: 1
   :stub-columns: 1

   * - Think Time
     - Duration [s]
     - Machine Energy [J]
     - CPU Energy [J]
     - Memory Energy [J]
     - Network Energy [J]
     - SCI [mgCO2e/order]
   * - `0 <https://metrics.green-coding.berlin/stats.html?id=25614e23-d474-4953-a08b-3808f8e46fe6>`__
     - 5.82
     - 181.52
     - 85.83
     - 5.40
     - 1.02
     - 34.2
   * - `1 <https://metrics.green-coding.berlin/stats.html?id=3849a50a-05ad-4345-9172-abf402ef5810>`__
     - 6.81
     - 195.18
     - 84.93
     - 5.71
     - 1.03
     - 37.7
   * - `2 <https://metrics.green-coding.berlin/stats.html?id=1b760419-456b-489d-b462-7d0201894a3c>`__
     - 7.83
     - 214.53
     - 90.22
     - 6.42
     - 1.03
     - 42.1
   * - `10 <https://metrics.green-coding.berlin/stats.html?id=6fd10682-c40b-4f48-a1a6-77bb80ecf7cd>`__
     - 15.66
     - 319.88
     - 94.31
     - 9.77
     - 1.06
     - 69.7

Differences Machine Energy to base (0 sec):

.. list-table::
   :header-rows: 1
   :align: left

   * - 1 sec
     - 2 sec
     - 10 sec
   * - +13.66 J (+7.5 %)
     - +33.01 J (+18.2 %)
     - +138.36 J (+76.2 %)

Differences CPU Energy to base (0 sec):

.. list-table::
   :header-rows: 1
   :align: left

   * - 1 sec
     - 2 sec
     - 10 sec
   * - -0,9 J (-1 %)
     - +4.4 J (+5,1 %)
     - +8.5 J (+9,9 %)

**Findings:**

* One additional sec think time increases the machine energy consumption by ~13-15 J and the cpu energy consumption by 4-5 J (idle consumption per second)

Load Test (high CPU utilization)
--------------------------------

**Research questions:**

* Is the total energy consumption proportional to the parallel users?
* Is the CPU energy consumption proportional to the parallel users?
* Is the memory energy consumption proportional to the parallel users?
* Is the energy consumption proportional to the CPU utilization?

**Scenario:** Many users in parallel: Each user checks out the inventory, think for 30-60 sec, add a random product to cart (3 times) and finally confirms the order. Logging of JMeter requests is disabled.

**Duration & Pre-Configured Ramp-up Times:**

.. list-table::
   :header-rows: 1
   :stub-columns: 1
   :align: left

   * - Number of Users
     - Duration [s]
     - Ramp-up time [s]
   * - `100 <https://metrics.green-coding.berlin/stats.html?id=9c29b4e9-7ee5-416e-9be5-6d183f14e3fc>`__
     - 186.26
     - 2
   * - `200 <https://metrics.green-coding.berlin/stats.html?id=eb85a781-4e7b-4570-a7bb-b9cd98ab7ebb>`__
     - 181.97
     - 2
   * - `300 <https://metrics.green-coding.berlin/stats.html?id=2737a2e8-677c-43c0-a167-57f7e9495160>`__
     - 175.22
     - 5
   * - `400 <https://metrics.green-coding.berlin/stats.html?id=1797131a-8bf2-44af-a845-f5fc462e6de0>`__
     - 180.08
     - 5
   * - `500 <https://metrics.green-coding.berlin/stats.html?id=d213415f-584c-407e-ab3b-ebc7c911df30>`__
     - 182.32
     - 5

**Energy Consumption:**

.. list-table::
   :header-rows: 1
   :stub-columns: 1
   :align: left

   * - Number of Users
     - Machine Power [W]
     - Machine Energy [J]
     - CPU Energy [J]
     - Memory Energy [J]
     - Network Energy [J]
   * - `100 <https://metrics.green-coding.berlin/stats.html?id=9c29b4e9-7ee5-416e-9be5-6d183f14e3fc>`__
     - 15.83
     - 2949.27
     - 370.25
     - 94.94
     - 311.21
   * - `200 <https://metrics.green-coding.berlin/stats.html?id=eb85a781-4e7b-4570-a7bb-b9cd98ab7ebb>`__
     - 16.42
     - 2990.24
     - 449.09
     - 99.10
     - 844.34
   * - `300 <https://metrics.green-coding.berlin/stats.html?id=2737a2e8-677c-43c0-a167-57f7e9495160>`__
     - 17.18
     - 3009.78
     - 513.25
     - 100.76
     - 1608.60
   * - `400 <https://metrics.green-coding.berlin/stats.html?id=1797131a-8bf2-44af-a845-f5fc462e6de0>`__
     - 17.66
     - 3180.31
     - 610.23
     - 108.03
     - 2588.05
   * - `500 <https://metrics.green-coding.berlin/stats.html?id=d213415f-584c-407e-ab3b-ebc7c911df30>`__
     - 18.43
     - 3360.63
     - 687.72
     - 113.05
     - 3781.67

Differences Machine Power:

.. list-table::
   :header-rows: 1
   :align: left

   * - 100→200
     - 200→300
     - 300→400
     - 400→500
   * - +0.59 W
     - +0,76 W
     - +0,48 W
     - +0,77 W

Differences Machine Energy:

.. list-table::
   :header-rows: 1
   :align: left

   * - 100→200
     - 200→300
     - 300→400
     - 400→500
   * - +40.97 J
     - +19.54 J
     - +170,53 J
     - +180,32 J

Differences CPU Energy:

.. list-table::
   :header-rows: 1
   :align: left

   * - 100→200
     - 200→300
     - 300→400
     - 400→500
   * - +78.84 J
     - +64.16 J
     - +96.98 J
     - +77.49 J

**CPU Utilization & Memory Usage:**

.. list-table::
   :header-rows: 1
   :stub-columns: 1
   :align: left

   * - Number of Users
     - ``backend`` CPU Mean [%]
     - ``backend`` CPU Max [%]
     - ``backend`` Memory Mean [MB]
     - ``backend`` Memory Max [MB]
   * - `100 <https://metrics.green-coding.berlin/stats.html?id=9c29b4e9-7ee5-416e-9be5-6d183f14e3fc>`__
     - 4.33
     - 88.39
     - 541.01
     - 566.46
   * - `200 <https://metrics.green-coding.berlin/stats.html?id=eb85a781-4e7b-4570-a7bb-b9cd98ab7ebb>`__
     - 6.99
     - 84.38
     - 493.71
     - 527.79
   * - `300 <https://metrics.green-coding.berlin/stats.html?id=2737a2e8-677c-43c0-a167-57f7e9495160>`__
     - 9.60
     - 79.81
     - 482.71
     - 510.46
   * - `400 <https://metrics.green-coding.berlin/stats.html?id=1797131a-8bf2-44af-a845-f5fc462e6de0>`__
     - 11.42
     - 78.71
     - 551.73
     - 602.95
   * - `500 <https://metrics.green-coding.berlin/stats.html?id=d213415f-584c-407e-ab3b-ebc7c911df30>`__
     - 12.95
     - 87.42
     - 587.36
     - 637.42

Differences Mean CPU Utilization:

.. list-table::
   :header-rows: 1
   :align: left

   * - 100→200
     - 200→300
     - 300→400
     - 400→500
   * - +2.66
     - +2.61
     - +1.82
     - +1.53

**Findings:**

* CPU differences increases for every 100 users by 64-96 J

Microservices
=============

In this section the findings of executing different usage scenarios with the microservices implementation are discussed.

tbd.

Modulith vs. Microservices
==========================

Standard Usage Scenario
-----------------------

**Research question:** What is more energy efficient in the standard usage scenario with 1 user, monolith or microservices?

**Scenario:** One user checks out the inventory, thinks for 30 sec, adds a random product to cart, thinks again, add a second product, thinks again, add a third product, and finally confirms the order.

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
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=50008066-07ef-438e-a727-dfcaf1d1c46b>`__
     - 95.72
     - 15.09
     - 1444.10
     - 161.28
     - 46.23
     - 2.47
     - 35.9
   * - `Microservices <https://metrics.green-coding.berlin/stats.html?id=b3352d36-ba6e-4b9e-9e67-3b5d345a7ff7>`__
     - 106.01
     - 18.05
     - 1913.97
     - 359.95
     - 60.35
     - 18.43
     - 43.9

**Findings:**

* The monolith in the standard usage scenario with 1 user is more efficient than the microservices implementation.

Multiple executions
-------------------

**Research question:** What is more energy efficient in the simple scenario with 1 user, monolith or microservices?

**Scenario:** One user executes multiple orders one after another.

.. list-table::
   :header-rows: 1
   :stub-columns: 3

   * - Monolith / Microservices
     - Number of Executions
     - Think Time (pre-configured) [s]
     - Duration [s]
     - Machine Energy [J]
     - CPU Energy [J]
     - Memory Energy [J]
     - Network Energy [J]
     - SCI [mgCO2e/order]
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=f1e0171c-a5f6-4f24-b5e4-558fe334993c>`__
     - 0
     - 0
     - 3.81
     - 113.25
     - 53.19
     - 3.00
     - 0.00
     - N/A
   * - `Microservices <https://metrics.green-coding.berlin/stats.html?id=e6c84f8f-971e-4401-97b1-3cd75e57c4a9>`__
     - 0
     - 0
     - 4.01
     - 125.64
     - 55.92
     - 3.36
     - 0.46
     - N/A
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=25614e23-d474-4953-a08b-3808f8e46fe6>`__
     - 1
     - 0
     - 5.82
     - 181.52
     - 85.83
     - 5.40
     - 1.02
     - 34.2
   * - `Microservices <https://metrics.green-coding.berlin/stats.html?id=59ed4330-d15b-465f-933c-9a7d966802f0>`__
     - 1
     - 0
     - 16.56
     - 441.30
     - 164.29
     - 14.00
     - 4.74
     - 87.3
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=7e40ee3b-733e-4b66-aaba-e1e32a412a28>`__
     - 100
     - 0
     - 13.40
     - 393.86
     - 166.47
     - 13.51
     - 83.08
     - 0.8
   * - `Microservices <https://metrics.green-coding.berlin/stats.html?id=bf22a5c1-670b-4bd2-ba94-ad225cefe7c0>`__
     - 100
     - 0
     - 78.13
     - 1815.27
     - 572.10
     - 67.15
     - 330.28
     - 3.8
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=c8aca13e-428a-4616-8677-93db8ebb0259>`__
     - 100
     - 1
     - 113.50
     - 1809.81
     - 254.30
     - 58.08
     - 84.94
     - 4.4
   * - `Microservices <https://metrics.green-coding.berlin/stats.html?id=a372a5ed-cb11-45bd-9b4c-8ad626f451bd>`__
     - 100
     - 1
     - 175.16
     - 3457.65
     - 808.74
     - 115.46
     - 345.57
     - 7.6

**Findings:**

* In this basic scenario with 1 user, the microservices system consumes significantly more energy → monolith is more energy-efficient if there is no load
* Some services in the microservices system are always active (Kafka, Zookeeper, Eventuate CDC Service, Orchestrator) that communicate with each other. Therefore in the scenario with 0 executions there is still an energy consumption of 0.46 J due to the network communication.

Load Test (high CPU utilization)
--------------------------------

**Note: The measurements of the microservices system are currently in WIP!**

**Research questions:**

* What is more energy efficient in a load test scenario with many parallel users, monolith or microservices?
* How relevant is the CPU, memory and network?

**Scenario:** Many users in parallel: Each user checks out the inventory, think for 30-60 sec, add a random product to cart (3 times) and finally confirms the order. Logging of JMeter requests is disabled.

**Durations:**

.. list-table::
   :header-rows: 1
   :stub-columns: 2
   :align: left

   * - Monolith / Microservices
     - Number of Users
     - Ramp-up time (pre-configured) [s]
     - Duration [s]
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=9c29b4e9-7ee5-416e-9be5-6d183f14e3fc>`__
     - 100
     - 2
     - 186.26
   * - `Microservices <https://metrics.green-coding.berlin/stats.html?id=ed9b2b05-740e-4769-a533-15e21154dbb0>`__
     - 100
     - 2
     - 185.92
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=eb85a781-4e7b-4570-a7bb-b9cd98ab7ebb>`__
     - 200
     - 2
     - 181.97
   * - `Microservices <?>`__
     - 200
     - 2
     - 
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=2737a2e8-677c-43c0-a167-57f7e9495160>`__
     - 300
     - 5
     - 175.22
   * - `Microservices <https://metrics.green-coding.berlin/stats.html?id=2c2f7111-9eaf-42be-854a-3ccb71f41241>`__
     - 300
     - 5
     - 182.88
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=1797131a-8bf2-44af-a845-f5fc462e6de0>`__
     - 400
     - 5
     - 180.08
   * - `Microservices <?>`__
     - 400
     - 5
     - 
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=d213415f-584c-407e-ab3b-ebc7c911df30>`__
     - 500
     - 5
     - 182.32
   * - `Microservices <?>`__
     - 100
     - 5
     - 

**Energy Consumption:**

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
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=9c29b4e9-7ee5-416e-9be5-6d183f14e3fc>`__
     - 100
     - 15.83
     - 2949.27
     - 370.25
     - 94.94
     - 311.21
   * - `Microservices <https://metrics.green-coding.berlin/stats.html?id=ed9b2b05-740e-4769-a533-15e21154dbb0>`__
     - 100
     - 20.93
     - 3891.40
     - 1050.28
     - 135.97
     - 717.14
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=eb85a781-4e7b-4570-a7bb-b9cd98ab7ebb>`__
     - 200
     - 16.42
     - 2990.24
     - 449.09
     - 99.10
     - 844.34
   * - `Microservices <?>`__
     - 200
     - 
     - 
     - 
     - 
     - 
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=2737a2e8-677c-43c0-a167-57f7e9495160>`__
     - 300
     - 17.18
     - 3009.78
     - 513.25
     - 100.76
     - 1608.60
   * - `Microservices <https://metrics.green-coding.berlin/stats.html?id=2c2f7111-9eaf-42be-854a-3ccb71f41241>`__
     - 300
     - 24.57
     - 4493.86
     - 1525.81
     - 173.44
     - 2402.92
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=1797131a-8bf2-44af-a845-f5fc462e6de0>`__
     - 400
     - 17.66
     - 3180.31
     - 610.23
     - 108.03
     - 2588.05
   * - `Microservices <?>`__
     - 400
     - 
     - 
     - 
     - 
     - 
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=d213415f-584c-407e-ab3b-ebc7c911df30>`__
     - 500
     - 18.43
     - 3360.63
     - 687.72
     - 113.05
     - 3781.67
   * - `Microservices <?>`__
     - 500
     - 
     - 
     - 
     - 
     - 

**CPU Utilization & Memory Usage:**

Note: JMeter is part of ``system``.

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
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=9c29b4e9-7ee5-416e-9be5-6d183f14e3fc>`__
     - 100
     - 7.52
     - 100.00
     - 1144.43
     - 1199.25
     - 741.55
   * - `Microservices <https://metrics.green-coding.berlin/stats.html?id=ed9b2b05-740e-4769-a533-15e21154dbb0>`__
     - 100
     - 27.23
     - 100.00
     - 3368.59
     - 3648.12
     - 2708.28
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=eb85a781-4e7b-4570-a7bb-b9cd98ab7ebb>`__
     - 200
     - 10.83
     - 100.00
     - 956.88
     - 1022.09
     - 505.19
   * - `Microservices <?>`__
     - 200
     - 
     - 
     - 
     - 
     - 
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=2737a2e8-677c-43c0-a167-57f7e9495160>`__
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
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=1797131a-8bf2-44af-a845-f5fc462e6de0>`__
     - 400
     - 17.15
     - 100.00
     - 1041.08
     - 1132.27
     - 536.1
   * - `Microservices <?>`__
     - 400
     - 
     - 
     - 
     - 
     - 
   * - `Monolith <https://metrics.green-coding.berlin/stats.html?id=d213415f-584c-407e-ab3b-ebc7c911df30>`__
     - 500
     - 19.97
     - 100.00
     - 1104.04
     - 1202.52
     - 507.04
   * - `Microservices <?>`__
     - 500
     - 
     - 
     - 
     - 
     - 

**Findings:**

* In these scenarios the Microservices system consumes a lot more energy
* Comparison in scenario 100 users:
   - Machine Energy: 2949 J vs. 3891 J (+32 %)
   - CPU Energy: 1050 J vs. 370 J (+184 %)
   - Memory Energy: 95 J vs. 136 J (+ 43 %) 
   - Network Energy: 311 J vs. 717 J (+131 %)
   - CPU Mean: 7.5 % vs. 27.2 %
   - Memory Mean: 1144 MB vs. 3369 MB
* Conclusion: This comparison is not fair → we need a more compute-intensive scenario
