.. _use:

======================
Usage
======================

The T2 Store has multiple aspects of usage.

- trigger slo violations with regard to response time and availability

to trigger and notice slo violations one doth require multiple things:

- monitoring and the instrumentation 
- load to get some values to monitor (we can not monitor any response time if no one uses the service.)

In addition there is a e2e-test-service that may be plugged in between uibackend and orchestrator.

sections

- description of monitoring instrumentation: prometheus, micrometer, endpoints


- triggering of slo violations: tweaking the respones time -> req. load generator + killing services with kubernetes / docker


Use
========================================

Step by Step 
------------

#. Run the E2E Test Service
#. Configure the UI Backend and the Payment Service 
#. Generate load
#. Look at the Logs 

Step 1 : Run E2E Test Service
-----------------------------

Run the `E2E Test Service <https://github.com/t2-project/e2e-tests>`__.
If you are on a kubernetes cluster, you may apply the deployment from the folder :file:`testsetup/` in the :file:`kube` repository.

.. code-block:: php

   kubectl apply -f testsetup/e2etest.yaml 

Step 2 : Configure the UI Backend and the Payment Service 
---------------------------------------------------------

Configure the UI Backend such that it sends confirmed orders to the Test service and configure the Payment service to send the payment requests to the Test service.

For Kubernetes
~~~~~~~~~~~~~~

In the UI Backend Deployment (:file:`uibackend.yml`):

.. code-block:: php

   - name: T2_ORCHESTRATOR_URL
     value: http://<e2e-test-host>/test/

In the Payment Deployment (:file:`payment.yml`):
   
.. code-block:: php

   - name: T2_PAYMENT_PROVIDER_DUMMY_URL
     value: http://<e2e-test-host>/fakepay

In both cases replace :file:`<e2e-test-host>` with the location of the Test Service.

Or use the deployment in the folder `testsetup <https://github.com/t2-project/kube/tree/main/testsetup>`__ because there the environment variables are already set as described above. 

Step 3 : Generate Load
-----------------------------

Confer the following section on how to generate load.
There must be some request or else there is nothing to test. 
The Test service does not generate load by itself.

Step 4 : Look at the Logs
-----------------------------

The Test results are printed to the logs. 
This might change but for now it is the easiest solution.


For Kubernetes
~~~~~~~~~~~~~~

.. code-block:: php

   kubectl logs <e2etest-pod>

Interpret Output
~~~~~~~~~~~~~~~~

A Test Report contains these Infomation:

*  **Expected Saga Status** : If it is :file:`FAILURE` then the saga instance supposed to have rolled back, other wise it should have run to completion.
*  **Saga Id** : Id of the Saga Instance in the Saga Instance DB. Used to look the Saga Instance up.
*  **Correlation Id** : Id used by the test service to correlate saga request to the Orchestrator with payment request from the Payment Service.
*  **Order**, **Inventory**, **Saga Instance** : Displays the test Result for the Order and Inventory service and the Saga Instance.


Report for Test that found every thing correct:

.. code-block:: php

   Test Report: 
       Expected Saga Status: FAILURE
       Saga Id: 000001796a7b7be5-7aef648a26a50000 Correlation Id: B42A90324D7639C1BCCC7A5E60080504
        Order: correct 
        Inventory: correct 
        Saga Instance: correct 

Report for Test that found that some entries in the inventory database were not deleted correctly:

.. code-block:: php

   Test Report: 
       Expected Saga Status: SUCCESS
       Saga Id: 000001796a7b7bde-7aef648a26a50000 Correlation Id: A79799BA296DF9035A11D1FF553D1AD2
        Order: correct 
        Inventory : reservations for sessionId A79799BA296DF9035A11D1FF553D1AD2 not deleted. ==> expected: <false> but was: <true>
        Saga Instance: correct 



Load Generation
===============

You can generate load manually by sending requests to the UIBackend (or using the UI, but it is ugly).
Confer the `UI Backend's README <https://github.com/t2-project/uibackend>`__ on how to talk to the UI Backend.

Or you can use a Load Generator to send request.
We recommend `Apache JMeter <https://jmeter.apache.org/>`__.

Apache JMeter
-------------

To run the T2 Store with the JMeter Load Generator, do the following :

#. Deploy the T2 Store
#. Make sure that the UI-Backend is accessible from outside the cluster - unless you want to put the load generator onto the cluster.
#. Install JMeter
#. Create or download a load profile
#. Run the load generator

Deploy T2 Store
~~~~~~~~~~~~~~~

Confer the previous sections on how to deploy the T2 Store.


~~~~~~~~~~~~~~~

e.g. on a unix : 
wget appache thing. --> java requirements?
unzip
wget load-profile-single
java -jar ...

explain parameters.

Other T2 store load profiles here : `<https://github.com/t2-project/kube/tree/main/loadprofiles>`__ 
They are explained below.

(Adapted from the `TeaStore Wiki <https://github.com/DescartesResearch/TeaStore/wiki/Testing-and-Benchmarking#22-jmeter>`__.)
 

Load Profiles
~~~~~~~~~~~~~

Random Infinite Load Profile
""""""""""""""""""""""""""""

The profile :file:`t2-store-random_infinite.jmx` generates requests to the UI Backend as visualized below.
Beware to set :file:`-Jhostname` and :file:`-Jport` to your UI Backend's address and port. 

.. image:: ../arch/figs/load_generator.jpg

With this profile the generator adds between 1 to 5 products to the cart, and confirm the order afterwards.
It chooses the product at random from the products in the inventory.


Fixed Single Load Profile
"""""""""""""""""""""""""

The profile :file:`t2-store-fixed_single.jmx` is similar to the previous one, but, as visualized below, it places only one order over 3 random products.

.. image:: ../arch/figs/load_generator_single.jpg

Prometheus
==========

The T2 Store can be monitored with `Prometheus <https://prometheus.io/>`__

The T2 Store services use `Micrometer <https://micrometer.io/docs/registry/prometheus>`__ to expose metrics endpoints for prometheus. 
Check the endpoint :file:`/actuator/prometheus` to see which metrics are exposed.

Jaeger / Opentracing
====================

Most of the  T2 store's services include the dependencies to be traced with `Jaeger <https://www.jaegertracing.io/>`__.