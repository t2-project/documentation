.. java:import:: com.fasterxml.jackson.annotation JsonCreator

.. java:import:: com.fasterxml.jackson.annotation JsonProperty

OrderRequest
============

.. java:package:: de.unistuttgart.t2.common
   :noindex:

.. java:type:: public class OrderRequest

   to be passed from ui to the ui backend.

   :author: maumau

Constructors
------------
OrderRequest
^^^^^^^^^^^^

.. java:constructor:: public OrderRequest()
   :outertype: OrderRequest

OrderRequest
^^^^^^^^^^^^

.. java:constructor:: @JsonCreator public OrderRequest(String cardNumber, String cardOwner, String checksum)
   :outertype: OrderRequest

Methods
-------
getCardNumber
^^^^^^^^^^^^^

.. java:method:: public String getCardNumber()
   :outertype: OrderRequest

getCardOwner
^^^^^^^^^^^^

.. java:method:: public String getCardOwner()
   :outertype: OrderRequest

getChecksum
^^^^^^^^^^^

.. java:method:: public String getChecksum()
   :outertype: OrderRequest

