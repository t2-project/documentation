SagaData
========

.. java:package:: de.unistuttgart.t2.common.saga
   :noindex:

.. java:type:: public class SagaData

   all the Data, that any saga participant might possibly need. the other option would be, that each saga participant collects its data from other services personally (e.g. payment again asks cart for which and what quantity of items were bought), but that is a lot of communication effort, thus biiig message. Payment wants: - payment info (creditcard stuff) - total money Inventory wants: - sessionid (to identify which reservations to delete) - (maybe) total for verification Order wants: - (nothing really) - but takes total, ordered units and products and, session id anyway.

Constructors
------------
SagaData
^^^^^^^^

.. java:constructor:: public SagaData(String cardNumber, String cardOwner, String checksum, String sessionId, String orderId, double total)
   :outertype: SagaData

SagaData
^^^^^^^^

.. java:constructor:: public SagaData(String cardNumber, String cardOwner, String checksum, String sessionId, double total)
   :outertype: SagaData

SagaData
^^^^^^^^

.. java:constructor:: public SagaData()
   :outertype: SagaData

Methods
-------
getCardNumber
^^^^^^^^^^^^^

.. java:method:: public String getCardNumber()
   :outertype: SagaData

getCardOwner
^^^^^^^^^^^^

.. java:method:: public String getCardOwner()
   :outertype: SagaData

getChecksum
^^^^^^^^^^^

.. java:method:: public String getChecksum()
   :outertype: SagaData

getOrderId
^^^^^^^^^^

.. java:method:: public String getOrderId()
   :outertype: SagaData

getSessionId
^^^^^^^^^^^^

.. java:method:: public String getSessionId()
   :outertype: SagaData

getTotal
^^^^^^^^

.. java:method:: public double getTotal()
   :outertype: SagaData

setOrderId
^^^^^^^^^^

.. java:method:: public void setOrderId(String orderId)
   :outertype: SagaData

