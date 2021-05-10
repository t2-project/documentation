.. java:import:: com.fasterxml.jackson.annotation JsonCreator

.. java:import:: com.fasterxml.jackson.annotation JsonProperty

ReservationRequest
==================

.. java:package:: de.unistuttgart.t2.common
   :noindex:

.. java:type:: public class ReservationRequest

   to be passed from ui backend to inventory.

   :author: maumau

Constructors
------------
ReservationRequest
^^^^^^^^^^^^^^^^^^

.. java:constructor:: public ReservationRequest()
   :outertype: ReservationRequest

ReservationRequest
^^^^^^^^^^^^^^^^^^

.. java:constructor:: @JsonCreator public ReservationRequest(String productId, String sessionId, int units)
   :outertype: ReservationRequest

Methods
-------
getProductId
^^^^^^^^^^^^

.. java:method:: public String getProductId()
   :outertype: ReservationRequest

getSessionId
^^^^^^^^^^^^

.. java:method:: public String getSessionId()
   :outertype: ReservationRequest

getUnits
^^^^^^^^

.. java:method:: public int getUnits()
   :outertype: ReservationRequest

