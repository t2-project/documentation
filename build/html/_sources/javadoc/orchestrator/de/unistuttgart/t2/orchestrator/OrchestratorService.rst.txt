.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: org.springframework.transaction.annotation Transactional

.. java:import:: de.unistuttgart.t2.common.saga SagaData

.. java:import:: de.unistuttgart.t2.orchestrator.saga Saga

.. java:import:: io.eventuate.tram.sagas.orchestration SagaInstance

.. java:import:: io.eventuate.tram.sagas.orchestration SagaInstanceFactory

OrchestratorService
===================

.. java:package:: de.unistuttgart.t2.orchestrator
   :noindex:

.. java:type:: public class OrchestratorService

   Manages creation of new saga instances.

   :author: maumau

Constructors
------------
OrchestratorService
^^^^^^^^^^^^^^^^^^^

.. java:constructor:: public OrchestratorService(SagaInstanceFactory sagaInstanceFactory, Saga saga)
   :outertype: OrchestratorService

Methods
-------
createSaga
^^^^^^^^^^

.. java:method:: @Transactional protected String createSaga(SagaData data)
   :outertype: OrchestratorService

   Creates a new saga instance.

   :param data: informations to be passed to all participants
   :return: id of saga instance

