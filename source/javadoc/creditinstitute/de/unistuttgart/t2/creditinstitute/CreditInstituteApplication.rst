.. java:import:: org.springframework.boot SpringApplication

.. java:import:: org.springframework.boot.autoconfigure EnableAutoConfiguration

.. java:import:: org.springframework.boot.autoconfigure SpringBootApplication

.. java:import:: org.springframework.context.annotation Bean

CreditInstituteApplication
==========================

.. java:package:: de.unistuttgart.t2.creditinstitute
   :noindex:

.. java:type:: @EnableAutoConfiguration @SpringBootApplication public class CreditInstituteApplication

   A dummy credit institute.

   This credit institute provides a very fake payment.

   :author: maumau

Methods
-------
main
^^^^

.. java:method:: public static void main(String[] args)
   :outertype: CreditInstituteApplication

service
^^^^^^^

.. java:method:: @Bean public CreditInstituteService service()
   :outertype: CreditInstituteApplication

