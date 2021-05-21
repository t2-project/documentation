.. java:import:: java.time Instant

.. java:import:: java.util ArrayList

.. java:import:: java.util Date

.. java:import:: java.util HashMap

.. java:import:: java.util List

.. java:import:: java.util Map

.. java:import:: java.util Optional

.. java:import:: javax.annotation PostConstruct

.. java:import:: org.slf4j Logger

.. java:import:: org.slf4j LoggerFactory

.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: org.springframework.beans.factory.annotation Value

.. java:import:: org.springframework.scheduling.concurrent ThreadPoolTaskScheduler

.. java:import:: org.springframework.stereotype Component

.. java:import:: org.springframework.transaction.annotation Transactional

TimeoutCollector.RecervationCheckAndDeleteTask
==============================================

.. java:package:: de.unistuttgart.t2.inventory.repository
   :noindex:

.. java:type:: protected class RecervationCheckAndDeleteTask implements Runnable
   :outertype: TimeoutCollector

   The Task that does the actual checking and deleting of reservations.

   :author: maumau

Methods
-------
run
^^^

.. java:method:: @Override public void run()
   :outertype: TimeoutCollector.RecervationCheckAndDeleteTask

