.. java:import:: org.springframework.boot SpringApplication

.. java:import:: org.springframework.boot.autoconfigure SpringBootApplication

.. java:import:: org.springframework.context.annotation Bean

.. java:import:: org.springframework.data.mongodb.repository.config EnableMongoRepositories

.. java:import:: org.springframework.scheduling.concurrent ThreadPoolTaskScheduler

.. java:import:: de.unistuttgart.t2.cart.repository CartRepository

CartApplication
===============

.. java:package:: de.unistuttgart.t2.cart
   :noindex:

.. java:type:: @SpringBootApplication @EnableMongoRepositories public class CartApplication

   Manages the products in the users carts.

   Users are distinguished by their session's ids.

   Neither controller nor Service because all endpoints are generated.

   :author: maumau

Methods
-------
main
^^^^

.. java:method:: public static void main(String[] args)
   :outertype: CartApplication

threadPoolTaskScheduler
^^^^^^^^^^^^^^^^^^^^^^^

.. java:method:: @Bean public ThreadPoolTaskScheduler threadPoolTaskScheduler()
   :outertype: CartApplication

