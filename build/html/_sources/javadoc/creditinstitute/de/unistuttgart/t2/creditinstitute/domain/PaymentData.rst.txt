.. java:import:: com.fasterxml.jackson.annotation JsonCreator

.. java:import:: com.fasterxml.jackson.annotation JsonProperty

PaymentData
===========

.. java:package:: de.unistuttgart.t2.creditinstitute.domain
   :noindex:

.. java:type:: public class PaymentData

   All the informations usually found on a credit card.

   :author: maumau

Constructors
------------
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

