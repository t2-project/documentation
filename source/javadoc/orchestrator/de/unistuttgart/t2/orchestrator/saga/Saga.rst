.. java:import:: org.slf4j Logger

.. java:import:: org.slf4j LoggerFactory

.. java:import:: de.unistuttgart.t2.common.saga OrderCreatedReply

.. java:import:: de.unistuttgart.t2.common.saga SagaData

.. java:import:: io.eventuate.tram.commands.common Success

.. java:import:: io.eventuate.tram.commands.consumer CommandWithDestination

.. java:import:: io.eventuate.tram.commands.consumer CommandWithDestinationBuilder

.. java:import:: io.eventuate.tram.sagas.orchestration SagaDefinition

.. java:import:: io.eventuate.tram.sagas.simpledsl SimpleSaga

Saga
====

.. java:package:: de.unistuttgart.t2.orchestrator.saga
   :noindex:

.. java:type:: public class Saga implements SimpleSaga<SagaData>

   Definition of the saga.

   For each saga definition exists a \ :java:ref:`SagaManager <io.eventuate.tram.sagas.orchestration.SagaManager>`\ , that manages the instances of the saga and executes the actions and compensations as defined in the saga.

   This saga has three participants: inventory, payment and order.

   Order for creating and rejecting and orders, payment for executing the payment (payment is the pivot step) and inventory to manage the product's stockpiles.

   :author: maumau

Methods
-------
getSagaDefinition
^^^^^^^^^^^^^^^^^

.. java:method:: @Override public SagaDefinition<SagaData> getSagaDefinition()
   :outertype: Saga

