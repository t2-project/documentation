.. java:import:: com.fasterxml.jackson.annotation JsonCreator

.. java:import:: com.fasterxml.jackson.annotation JsonProperty

SagaRequest
===========

.. java:package:: de.unistuttgart.t2.common
   :noindex:

.. java:type:: public class SagaRequest

   Request to start a saga.

   Holds all the information that are necessary for the saga. That is information about the payment method and the costs, and the sessionId to identify the users. all the Data, that any saga participant might possibly

   Used to communicate with the orchestrator service.

Constructors
------------
SagaRequest
^^^^^^^^^^^

.. java:constructor:: public SagaRequest()
   :outertype: SagaRequest

SagaRequest
^^^^^^^^^^^

.. java:constructor:: @JsonCreator public SagaRequest(String sessionId, String cardNumber, String cardOwner, String checksum, double total)
   :outertype: SagaRequest

Methods
-------
getCardNumber
^^^^^^^^^^^^^

.. java:method:: public String getCardNumber()
   :outertype: SagaRequest

getCardOwner
^^^^^^^^^^^^

.. java:method:: public String getCardOwner()
   :outertype: SagaRequest

getChecksum
^^^^^^^^^^^

.. java:method:: public String getChecksum()
   :outertype: SagaRequest

getSessionId
^^^^^^^^^^^^

.. java:method:: public String getSessionId()
   :outertype: SagaRequest

getTotal
^^^^^^^^

.. java:method:: public double getTotal()
   :outertype: SagaRequest

toString
^^^^^^^^

.. java:method:: @Override public String toString()
   :outertype: SagaRequest

