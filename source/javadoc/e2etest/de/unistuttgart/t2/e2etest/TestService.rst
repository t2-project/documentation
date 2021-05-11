.. java:import:: java.util HashSet

.. java:import:: java.util List

.. java:import:: java.util Map

.. java:import:: java.util Optional

.. java:import:: java.util Set

.. java:import:: java.util.concurrent ConcurrentHashMap

.. java:import:: java.util.concurrent TimeoutException

.. java:import:: org.slf4j Logger

.. java:import:: org.slf4j LoggerFactory

.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: org.springframework.beans.factory.annotation Value

.. java:import:: org.springframework.stereotype Component

.. java:import:: org.springframework.web.client RestTemplate

.. java:import:: com.fasterxml.jackson.core JsonProcessingException

.. java:import:: com.fasterxml.jackson.databind JsonMappingException

.. java:import:: com.fasterxml.jackson.databind JsonNode

.. java:import:: com.fasterxml.jackson.databind ObjectMapper

.. java:import:: de.unistuttgart.t2.common SagaRequest

.. java:import:: de.unistuttgart.t2.inventory.repository InventoryItem

.. java:import:: de.unistuttgart.t2.inventory.repository ProductRepository

.. java:import:: de.unistuttgart.t2.order.repository OrderItem

.. java:import:: de.unistuttgart.t2.order.repository OrderRepository

.. java:import:: de.unistuttgart.t2.order.repository OrderStatus

.. java:import:: io.eventuate.tram.sagas.orchestration SagaInstance

.. java:import:: io.eventuate.tram.sagas.orchestration SagaInstanceRepository

TestService
===========

.. java:package:: de.unistuttgart.t2.e2etest
   :noindex:

.. java:type:: @Component public class TestService

   Responsible for asserting that the T2 store's state is in the end always correct.

   :author: maumau

Fields
------
correlationToSaga
^^^^^^^^^^^^^^^^^

.. java:field:: public Map<String, String> correlationToSaga
   :outertype: TestService

correlationToStatus
^^^^^^^^^^^^^^^^^^^

.. java:field:: public Map<String, OrderStatus> correlationToStatus
   :outertype: TestService

inprogress
^^^^^^^^^^

.. java:field:: public Set<String> inprogress
   :outertype: TestService

Methods
-------
postToOrchestrator
^^^^^^^^^^^^^^^^^^

.. java:method:: public String postToOrchestrator(SagaRequest request)
   :outertype: TestService

   Post saga request to the orchestrator.

   :param request: the request to send
   :return: id of started saga instance

sagaRuntimeTest
^^^^^^^^^^^^^^^

.. java:method:: public void sagaRuntimeTest(String correlationid)
   :outertype: TestService

   Tests the T2 stores state at runtime.

   :param correlationid: to identify the saga instance

