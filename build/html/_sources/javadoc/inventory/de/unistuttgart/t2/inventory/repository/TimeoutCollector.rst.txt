.. java:import:: java.time Instant

.. java:import:: java.util Collection

.. java:import:: java.util Date

.. java:import:: java.util List

.. java:import:: java.util.stream Collectors

.. java:import:: javax.annotation PostConstruct

.. java:import:: org.slf4j Logger

.. java:import:: org.slf4j LoggerFactory

.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: org.springframework.beans.factory.annotation Value

.. java:import:: org.springframework.scheduling.concurrent ThreadPoolTaskScheduler

.. java:import:: org.springframework.stereotype Component

TimeoutCollector
================

.. java:package:: de.unistuttgart.t2.inventory.repository
   :noindex:

.. java:type:: @Component public class TimeoutCollector

   Periodically checks all reservations and deletes those whose time to life has been exceeded. TODO : ensure that only reservations that are not part of a running saga are deleted

   :author: maumau

Constructors
------------
TimeoutCollector
^^^^^^^^^^^^^^^^

.. java:constructor:: @Autowired public TimeoutCollector(long TTL, int taskRate, ThreadPoolTaskScheduler taskScheduler, ReservationRepository repository, ProductRepository itemRepository)
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

