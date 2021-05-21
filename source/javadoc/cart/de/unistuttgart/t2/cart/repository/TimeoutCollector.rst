.. java:import:: java.time Instant

.. java:import:: java.util ArrayList

.. java:import:: java.util Date

.. java:import:: java.util List

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

.. java:package:: de.unistuttgart.t2.cart.repository
   :noindex:

.. java:type:: @Component public class TimeoutCollector

   Periodically checks all reservations and deletes those whose time to life has been exceeded.

   (apparently there is a mongo native attach on expiry date to documents, but i didn't find anything on whether this also works with the spring repository interface. thus the manual deletion.)

   :author: maumau

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
scheduleTask
^^^^^^^^^^^^

.. java:method:: @PostConstruct public void scheduleTask()
   :outertype: TimeoutCollector

   Schedule the task to check cart contents and delete them if necessary.

   If the taskRate is 0, no task will be scheduled.

