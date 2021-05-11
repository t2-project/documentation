.. java:import:: com.fasterxml.jackson.annotation JsonCreator

.. java:import:: com.fasterxml.jackson.annotation JsonProperty

SagaRequest
===========

.. java:package:: de.unistuttgart.t2.common.saga
   :noindex:

.. java:type:: public class SagaRequest

   all the Data, that any saga participant might possibly need. for passing from uibackend to orchestrator this is a separate class even though the content is literally the same as in \ :java:ref:`SagaData`\  such that i can change the communication backend - orchestrator and orchestrator - participants independently of each other. also i dont want to clutter my saga data with those json annotations.

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

setCardNumber
^^^^^^^^^^^^^

.. java:method:: public void setCardNumber(String cardNumber)
   :outertype: SagaRequest

setCardOwner
^^^^^^^^^^^^

.. java:method:: public void setCardOwner(String cardOwner)
   :outertype: SagaRequest

setChecksum
^^^^^^^^^^^

.. java:method:: public void setChecksum(String checksum)
   :outertype: SagaRequest

setSessionId
^^^^^^^^^^^^

.. java:method:: public void setSessionId(String sessionId)
   :outertype: SagaRequest

setTotal
^^^^^^^^

.. java:method:: public void setTotal(double total)
   :outertype: SagaRequest

toString
^^^^^^^^

.. java:method:: @Override public String toString()
   :outertype: SagaRequest

