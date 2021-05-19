.. java:import:: org.springframework.boot SpringApplication

.. java:import:: org.springframework.boot.autoconfigure SpringBootApplication

.. java:import:: org.springframework.boot.builder SpringApplicationBuilder

.. java:import:: org.springframework.boot.web.servlet.support SpringBootServletInitializer

.. java:import:: org.springframework.context.annotation Bean

.. java:import:: org.springframework.web.client RestTemplate

WebuiApplication
================

.. java:package:: de.unistuttgart.t2.ui.webui.app
   :noindex:

.. java:type:: @SpringBootApplication public class WebuiApplication extends SpringBootServletInitializer

   WebUi for the human user. It talks to the UI Backend.

   :author: maumau

Methods
-------
configure
^^^^^^^^^

.. java:method:: @Override protected SpringApplicationBuilder configure(SpringApplicationBuilder builder)
   :outertype: WebuiApplication

main
^^^^

.. java:method:: public static void main(String[] args)
   :outertype: WebuiApplication

template
^^^^^^^^

.. java:method:: @Bean public RestTemplate template()
   :outertype: WebuiApplication

