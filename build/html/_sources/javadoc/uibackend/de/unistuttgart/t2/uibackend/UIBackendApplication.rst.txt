.. java:import:: org.springframework.beans.factory.annotation Value

.. java:import:: org.springframework.boot SpringApplication

.. java:import:: org.springframework.boot.autoconfigure SpringBootApplication

.. java:import:: org.springframework.context.annotation Bean

.. java:import:: org.springframework.web.client RestTemplate

UIBackendApplication
====================

.. java:package:: de.unistuttgart.t2.uibackend
   :noindex:

.. java:type:: @SpringBootApplication public class UIBackendApplication

   Interacts with other services to prepare data for the actual UI. (If did it right, this service is a API Gateway)

   :author: maumau

Methods
-------
backendService
^^^^^^^^^^^^^^

.. java:method:: @Bean public UIBackendService backendService()
   :outertype: UIBackendApplication

main
^^^^

.. java:method:: public static void main(String[] args)
   :outertype: UIBackendApplication

template
^^^^^^^^

.. java:method:: @Bean public RestTemplate template()
   :outertype: UIBackendApplication

