.. java:import:: org.slf4j Logger

.. java:import:: org.slf4j LoggerFactory

.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: org.springframework.beans.factory.annotation Value

.. java:import:: org.springframework.web.client RestTemplate

.. java:import:: de.unistuttgart.t2.common.saga SagaData

.. java:import:: io.github.resilience4j.retry Retry

.. java:import:: io.github.resilience4j.retry RetryConfig

.. java:import:: io.github.resilience4j.retry RetryRegistry

PaymentService
==============

.. java:package:: de.unistuttgart.t2.payment
   :noindex:

.. java:type:: public class PaymentService

   Contacts a payment provider, e.g. some credit institute, to execute the payment.

   :author: maumau

Fields
------
config
^^^^^^

.. java:field::  RetryConfig config
   :outertype: PaymentService

providerUrl
^^^^^^^^^^^

.. java:field:: @Value protected String providerUrl
   :outertype: PaymentService

registry
^^^^^^^^

.. java:field::  RetryRegistry registry
   :outertype: PaymentService

retry
^^^^^

.. java:field::  Retry retry
   :outertype: PaymentService

template
^^^^^^^^

.. java:field:: @Autowired  RestTemplate template
   :outertype: PaymentService

Methods
-------
handleSagaAction
^^^^^^^^^^^^^^^^

.. java:method:: public void handleSagaAction(SagaData data)
   :outertype: PaymentService

   contact some payment provider to execute the payment. the call might either timeout, or the payment itself might fail, or it is successful.

   :param data: information about payment

