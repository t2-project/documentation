.. java:import:: org.springframework.boot.autoconfigure EnableAutoConfiguration

.. java:import:: org.springframework.context.annotation Bean

.. java:import:: org.springframework.context.annotation Configuration

.. java:import:: org.springframework.data.mongodb.repository.config EnableMongoRepositories

.. java:import:: de.unistuttgart.t2.order.repository OrderRepository

TestContext
===========

.. java:package:: de.unistuttgart.t2.order
   :noindex:

.. java:type:: @Configuration @EnableMongoRepositories public class TestContext

Methods
-------
service
^^^^^^^

.. java:method:: @Bean public OrderService service()
   :outertype: TestContext

