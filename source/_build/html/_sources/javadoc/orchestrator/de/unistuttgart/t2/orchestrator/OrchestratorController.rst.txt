.. java:import:: org.slf4j Logger

.. java:import:: org.slf4j LoggerFactory

.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: org.springframework.http HttpStatus

.. java:import:: org.springframework.web.bind.annotation PostMapping

.. java:import:: org.springframework.web.bind.annotation RequestBody

.. java:import:: org.springframework.web.bind.annotation ResponseStatus

.. java:import:: org.springframework.web.bind.annotation RestController

.. java:import:: de.unistuttgart.t2.common.saga SagaData

.. java:import:: de.unistuttgart.t2.common.saga SagaRequest

OrchestratorController
======================

.. java:package:: de.unistuttgart.t2.orchestrator
   :noindex:

.. java:type:: @RestController public class OrchestratorController

   Defines the http enpoints of the orchestrator service.

   :author: maumau

Fields
------
service
^^^^^^^

.. java:field:: @Autowired  OrchestratorService service
   :outertype: OrchestratorController

Methods
-------
createOrder
^^^^^^^^^^^

.. java:method:: @ResponseStatus @PostMapping public String createOrder(SagaRequest request)
   :outertype: OrchestratorController

   Starts a saga.

   Replies as soon as the saga is created.

   :param request: request to start a saga
   :return: id of saga instance

