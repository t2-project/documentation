.. java:import:: org.springframework.boot SpringApplication

.. java:import:: org.springframework.boot.autoconfigure EnableAutoConfiguration

.. java:import:: org.springframework.boot.autoconfigure SpringBootApplication

.. java:import:: org.springframework.context.annotation Bean

.. java:import:: org.springframework.context.annotation Configuration

.. java:import:: org.springframework.context.annotation Import

.. java:import:: org.springframework.data.jpa.repository.config EnableJpaRepositories

.. java:import:: org.springframework.data.mongodb.repository.config EnableMongoRepositories

.. java:import:: org.springframework.web.client RestTemplate

.. java:import:: de.unistuttgart.t2.inventory.repository ProductRepository

.. java:import:: de.unistuttgart.t2.order.repository OrderRepository

.. java:import:: io.eventuate.tram.sagas.orchestration SagaInstanceRepository

.. java:import:: io.eventuate.tram.sagas.spring.orchestration SagaOrchestratorConfiguration

.. java:import:: io.eventuate.tram.spring.consumer.kafka EventuateTramKafkaMessageConsumerConfiguration

.. java:import:: io.eventuate.tram.spring.messaging.producer.jdbc TramMessageProducerJdbcConfiguration

TestApplication
===============

.. java:package:: de.unistuttgart.t2.e2etest
   :noindex:

.. java:type:: @Configuration @EnableJpaRepositories @EnableAutoConfiguration @Import @EnableMongoRepositories @SpringBootApplication public class TestApplication

   Tests the entire T2 store.

   Needs all those saga configuration because \ :java:ref:`TestService`\  uses the \ :java:ref:`SagaInstanceRepository`\  Interface from the eventuate framework to access the saga instance database.

   :author: maumau

Methods
-------
getRestTemplate
^^^^^^^^^^^^^^^

.. java:method:: @Bean public RestTemplate getRestTemplate()
   :outertype: TestApplication

main
^^^^

.. java:method:: public static void main(String[] args)
   :outertype: TestApplication

