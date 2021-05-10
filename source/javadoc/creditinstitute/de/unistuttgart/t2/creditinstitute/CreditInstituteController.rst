.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: org.springframework.web.bind.annotation GetMapping

.. java:import:: org.springframework.web.bind.annotation PathVariable

.. java:import:: org.springframework.web.bind.annotation PostMapping

.. java:import:: org.springframework.web.bind.annotation RequestBody

.. java:import:: org.springframework.web.bind.annotation RestController

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

setFailurerate
^^^^^^^^^^^^^^

.. java:method:: @GetMapping public double setFailurerate(String rate)
   :outertype: CreditInstituteController

   Updated and get the failure rate.

   If the parameter cannot be processed, the rate remains unchanged.

   :param rate: new failure rate
   :return: current failure rate

setTimeout
^^^^^^^^^^

.. java:method:: @GetMapping public int setTimeout(String timeout)
   :outertype: CreditInstituteController

   Updated and get the timeout duration.

   If the parameter cannot be processed, the timeout remains unchanged.

   :param timeout: new timeout duration
   :return: current timeout duration

setTimeoutrate
^^^^^^^^^^^^^^

.. java:method:: @GetMapping public double setTimeoutrate(String rate)
   :outertype: CreditInstituteController

   Updated and get the timeout rate.

   If the parameter cannot be processed, the rate remains unchanged.

   :param rate: new timeout rate
   :return: current timeout rate

