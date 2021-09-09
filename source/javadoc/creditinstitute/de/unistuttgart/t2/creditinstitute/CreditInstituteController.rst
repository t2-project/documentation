.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: org.springframework.http HttpStatus

.. java:import:: org.springframework.http ResponseEntity

.. java:import:: org.springframework.web.bind.annotation ExceptionHandler

.. java:import:: org.springframework.web.bind.annotation GetMapping

.. java:import:: org.springframework.web.bind.annotation PostMapping

.. java:import:: org.springframework.web.bind.annotation RequestBody

.. java:import:: org.springframework.web.bind.annotation ResponseStatus

.. java:import:: org.springframework.web.bind.annotation RestController

.. java:import:: de.unistuttgart.t2.creditinstitute.domain PaymentData

.. java:import:: de.unistuttgart.t2.creditinstitute.exceptions PaymentFailedException

CreditInstituteController
=========================

.. java:package:: de.unistuttgart.t2.creditinstitute
   :noindex:

.. java:type:: @RestController public class CreditInstituteController

   Defines the endpoints of the credit institute.

   :author: maumau

Fields
------
service
^^^^^^^

.. java:field:: @Autowired  CreditInstituteService service
   :outertype: CreditInstituteController

Methods
-------
doPayment
^^^^^^^^^

.. java:method:: @PostMapping public void doPayment(PaymentData card) throws Exception
   :outertype: CreditInstituteController

   Fakes performs some payment.

   :param card: informations usually found on a credit card
   :throws Exception: if anything 'failed'

getFailurerate
^^^^^^^^^^^^^^

.. java:method:: @GetMapping public double getFailurerate()
   :outertype: CreditInstituteController

getTimeout
^^^^^^^^^^

.. java:method:: @GetMapping public int getTimeout()
   :outertype: CreditInstituteController

getTimeoutrate
^^^^^^^^^^^^^^

.. java:method:: @GetMapping public double getTimeoutrate()
   :outertype: CreditInstituteController

handleIllegalArgumentException
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. java:method:: @ExceptionHandler @ResponseStatus public ResponseEntity<String> handleIllegalArgumentException(IllegalArgumentException exception)
   :outertype: CreditInstituteController

   Creates the response entity if setting the timeout or the rates failed.

   :param exception:
   :return: a response entity with an exceptional message

handlePaymentFailedException
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. java:method:: @ExceptionHandler @ResponseStatus public ResponseEntity<String> handlePaymentFailedException(PaymentFailedException exception)
   :outertype: CreditInstituteController

   Creates the response entity if serving a payment request failed.

   :param exception:
   :return: a response entity with an exceptional message

setFailurerate
^^^^^^^^^^^^^^

.. java:method:: @PostMapping public double setFailurerate(double rate)
   :outertype: CreditInstituteController

   Updated and get the failure rate.

   If the parameter cannot be processed, the rate remains unchanged.

   :param rate: new failure rate
   :return: current failure rate

setTimeout
^^^^^^^^^^

.. java:method:: @PostMapping public int setTimeout(int timeout)
   :outertype: CreditInstituteController

   Updated and get the timeout duration.

   If the parameter cannot be processed, the timeout remains unchanged.

   :param timeout: new timeout duration
   :return: current timeout duration

setTimeoutrate
^^^^^^^^^^^^^^

.. java:method:: @PostMapping public double setTimeoutrate(double rate)
   :outertype: CreditInstituteController

   Updated and get the timeout rate.

   If the parameter cannot be processed, the rate remains unchanged.

   :param rate: new timeout rate
   :return: current timeout rate

