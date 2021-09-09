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

TimeoutCollector.RecervationCheckAndDeleteTask
==============================================

.. java:package:: de.unistuttgart.t2.inventory.repository
   :noindex:

.. java:type:: protected class RecervationCheckAndDeleteTask implements Runnable
   :outertype: TimeoutCollector

   The Task that does the actual checking and deleting of reservations. TODO how do i prevent this from collection 'in progress' sagas? TODO 'father less' reservations are only caused when orchestrator is down. I could flag the reservations as 'PENDING' (not yet ordered) 'PROCESSING' (saga runs) or 'DONE' (you may delete) and frequently delete 'DONE', scarcely delete 'PENDING' (i.e. after cookie death) and report 'PROCESSING' after some time as major erro...

   :author: maumau

Methods
-------
deleteAtItems
^^^^^^^^^^^^^

.. java:method:: public void deleteAtItems(Collection<Reservation> rs)
   :outertype: TimeoutCollector.RecervationCheckAndDeleteTask

run
^^^

.. java:method:: @Override public void run()
   :outertype: TimeoutCollector.RecervationCheckAndDeleteTask

