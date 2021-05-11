.. java:import:: java.time Duration

.. java:import:: org.springframework.beans.factory.annotation Value

.. java:import:: org.springframework.boot SpringApplication

.. java:import:: org.springframework.boot.autoconfigure EnableAutoConfiguration

.. java:import:: org.springframework.boot.autoconfigure SpringBootApplication

.. java:import:: org.springframework.boot.web.client RestTemplateBuilder

.. java:import:: org.springframework.context.annotation Bean

.. java:import:: org.springframework.context.annotation Import

.. java:import:: org.springframework.web.client RestTemplate

.. java:import:: de.unistuttgart.t2.payment.config ExcludeSagaConfig

.. java:import:: de.unistuttgart.t2.payment.config IncludeSagaConfig

PaymentApplication
==================

.. java:package:: de.unistuttgart.t2.payment
   :noindex:

.. java:type:: @Import @EnableAutoConfiguration @SpringBootApplication public class PaymentApplication

Fields
------
timeout
^^^^^^^

.. java:field:: @Value public int timeout
   :outertype: PaymentApplication

Methods
-------
main
^^^^

.. java:method:: public static void main(String[] args)
   :outertype: PaymentApplication

paymentService
^^^^^^^^^^^^^^

.. java:method:: @Bean public PaymentService paymentService()
   :outertype: PaymentApplication

template
^^^^^^^^

.. java:method:: @Bean public RestTemplate template(RestTemplateBuilder restTemplateBuilder)
   :outertype: PaymentApplication

