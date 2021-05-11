.. java:import:: java.util Random

.. java:import:: org.slf4j Logger

.. java:import:: org.slf4j LoggerFactory

.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: org.springframework.http HttpStatus

.. java:import:: org.springframework.http ResponseEntity

.. java:import:: org.springframework.web.bind.annotation ExceptionHandler

.. java:import:: org.springframework.web.bind.annotation PostMapping

.. java:import:: org.springframework.web.bind.annotation RequestBody

.. java:import:: org.springframework.web.bind.annotation ResponseStatus

.. java:import:: org.springframework.web.bind.annotation RestController

.. java:import:: de.unistuttgart.t2.common SagaRequest

.. java:import:: de.unistuttgart.t2.e2etest.exception FakeFailureException

.. java:import:: de.unistuttgart.t2.order.repository OrderStatus

.. java:import:: de.unistuttgart.t2.payment PaymentData

TestController
==============

.. java:package:: de.unistuttgart.t2.e2etest
   :noindex:

.. java:type:: @RestController public class TestController

   Defines endpoints for the e2e test.

   The e2e test is intercepts the t2 store at two points. First it takes the \ :java:ref:`SagaRequest <de.unistuttgart.t2.common.SagaRequest>`\  from the UIBackend to the orchestrator, and then it takes the requests that the payment service posts. This way the e2e test knows what reply the payment service received and thus also knows whether the saga instance is supposed to succeed or not.

   :author: maumau

Fields
------
service
^^^^^^^

.. java:field:: @Autowired  TestService service
   :outertype: TestController

Methods
-------
fakepay
^^^^^^^

.. java:method:: @PostMapping public void fakepay(PaymentData paymentdata) throws Exception
   :outertype: TestController

   Fakes the reply to the payment service and start a thread that asserts the saga instance.

   The payment service request payment for each saga instance. If that request fails, the service tries again. This endpoints replies are consistent for a request and its retries.

   Also the assertion thing is triggered only once for each saga instance. There is no need to check the same thing twice.

   As described in \ :java:ref:`TestController.test(SagaRequest)`\ , the field \ ``checksum``\  hold an id to correlate the payment request to the saga instance.

   :param paymentdata: request data. the \ ``checksum``\  is the with correlation id
   :throws Exception: if payment 'failed'

handleFakeFailureException
^^^^^^^^^^^^^^^^^^^^^^^^^^

.. java:method:: @ExceptionHandler @ResponseStatus public ResponseEntity<String> handleFakeFailureException(FakeFailureException exception)
   :outertype: TestController

   Creates the response entity in case of faked failure.

   :param exception:
   :return: a response entity with an exceptional message

test
^^^^

.. java:method:: @ResponseStatus @PostMapping public void test(SagaRequest request)
   :outertype: TestController

   Intercepts the communication from the UIBackend to the orchestrator.

   Takes the \ ``request``\  that from UIBackend and modifies it such that it might be correlated to an incoming payment request. Also sets what reply said payment request will receive and forward finally forwards the request to the orchestrator.

   As only the information about the credit cart will end up in the request to the payment provider, the field \ ``checksum``\  will be miss used to correlate the payment requests received in \ :java:ref:`TestController.fakepay(PaymentData)`\  to the saga request reveiced in this operation.

   It would have been pretty cool, if i could just put the saga id into the request but i cannot because i only get the saga id after i post the request to the orchestrator.

   :param request: intended for orchestrator

