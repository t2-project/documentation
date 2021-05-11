.. java:import:: com.fasterxml.jackson.annotation JsonCreator

.. java:import:: com.fasterxml.jackson.annotation JsonProperty

PaymentData
===========

.. java:package:: de.unistuttgart.t2.payment
   :noindex:

.. java:type:: public class PaymentData

   All information that must be sent to the payment provider. This includes information about the credit cart and the total amount of money to be paid.

   :author: maumau

Constructors
------------
PaymentData
^^^^^^^^^^^

.. java:constructor:: public PaymentData()
   :outertype: PaymentData

PaymentData
^^^^^^^^^^^

.. java:constructor:: @JsonCreator public PaymentData(String cardNumber, String cardOwner, String checksum, double total)
   :outertype: PaymentData

Methods
-------
getCardNumber
^^^^^^^^^^^^^

.. java:method:: public String getCardNumber()
   :outertype: PaymentData

getCardOwner
^^^^^^^^^^^^

.. java:method:: public String getCardOwner()
   :outertype: PaymentData

getChecksum
^^^^^^^^^^^

.. java:method:: public String getChecksum()
   :outertype: PaymentData

