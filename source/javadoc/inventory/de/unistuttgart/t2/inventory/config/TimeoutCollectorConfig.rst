.. java:import:: org.springframework.boot.autoconfigure EnableAutoConfiguration

.. java:import:: org.springframework.context.annotation Bean

.. java:import:: org.springframework.context.annotation Configuration

.. java:import:: org.springframework.scheduling.concurrent ThreadPoolTaskScheduler

.. java:import:: de.unistuttgart.t2.inventory.repository TimeoutCollector

TimeoutCollectorConfig
======================

.. java:package:: de.unistuttgart.t2.inventory.config
   :noindex:

.. java:type:: @EnableAutoConfiguration @Configuration public class TimeoutCollectorConfig

   Configuration to have all beans required for the \ :java:ref:`TimeoutCollector <TimeoutCollector>`\ .

   :author: maumau

Methods
-------
threadPoolTaskScheduler
^^^^^^^^^^^^^^^^^^^^^^^

.. java:method:: @Bean public ThreadPoolTaskScheduler threadPoolTaskScheduler()
   :outertype: TimeoutCollectorConfig

