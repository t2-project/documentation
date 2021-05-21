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

TimeoutCollector
================

.. java:package:: de.unistuttgart.t2.inventory.repository
   :noindex:

.. java:type:: @Component public class TimeoutCollector

   Periodically checks all reservations and deletes those whose time to life has been exceeded.

   (apparently there is a mongo native attach on expiry date to documents, but i didn't find anything on whether this also works with the spring repository interface. thus the manual deletion.)

   :author: maumau

Fields
------
repository
^^^^^^^^^^

.. java:field:: @Autowired  ProductRepository repository
   :outertype: TimeoutCollector

Constructors
------------
TimeoutCollector
^^^^^^^^^^^^^^^^

.. java:constructor:: @Autowired public TimeoutCollector(long TTL, int taskRate)
   :outertype: TimeoutCollector

   Create collector.

   :param TTL: the cart entries' time to live in seconds
   :param taskRate: rate at which the collector checks the repo in milliseconds

Methods
-------
schedulePeriodically
^^^^^^^^^^^^^^^^^^^^

.. java:method:: @PostConstruct public void schedulePeriodically()
   :outertype: TimeoutCollector

   Schedule the task to check reservations and delete them if necessary.

   If either the TTL or the taskRate is 0, no task will be scheduled.

