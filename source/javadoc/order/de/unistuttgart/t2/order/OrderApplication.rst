.. java:import:: org.springframework.boot SpringApplication

.. java:import:: org.springframework.boot.autoconfigure EnableAutoConfiguration

.. java:import:: org.springframework.boot.autoconfigure SpringBootApplication

.. java:import:: org.springframework.context.annotation Bean

.. java:import:: org.springframework.context.annotation Import

.. java:import:: org.springframework.data.jpa.repository.config EnableJpaRepositories

.. java:import:: org.springframework.data.mongodb.repository.config EnableMongoRepositories

.. java:import:: de.unistuttgart.t2.order.repository OrderRepository

.. java:import:: de.unistuttgart.t2.order.saga OrderCommandHandler

.. java:import:: io.eventuate.tram.sagas.participant SagaCommandDispatcher

.. java:import:: io.eventuate.tram.sagas.participant SagaCommandDispatcherFactory

.. java:import:: io.eventuate.tram.sagas.spring.participant SagaParticipantConfiguration

.. java:import:: io.eventuate.tram.spring.consumer.kafka EventuateTramKafkaMessageConsumerConfiguration

.. java:import:: io.eventuate.tram.spring.messaging.producer.jdbc TramMessageProducerJdbcConfiguration

.. java:import:: io.eventuate.tram.spring.optimisticlocking OptimisticLockingDecoratorConfiguration

OrderApplication
================

.. java:package:: de.unistuttgart.t2.order
   :noindex:

.. java:type:: @Import @EnableJpaRepositories @EnableAutoConfiguration @SpringBootApplication @EnableMongoRepositories public class OrderApplication

Methods
-------
main
^^^^

.. java:method:: public static void main(String[] args)
   :outertype: OrderApplication

orderCommandDispatcher
^^^^^^^^^^^^^^^^^^^^^^

.. java:method:: @Bean public SagaCommandDispatcher orderCommandDispatcher(OrderCommandHandler target, SagaCommandDispatcherFactory sagaCommandDispatcherFactory)
   :outertype: OrderApplication

orderCommandHandler
^^^^^^^^^^^^^^^^^^^

.. java:method:: @Bean public OrderCommandHandler orderCommandHandler()
   :outertype: OrderApplication

orderService
^^^^^^^^^^^^

.. java:method:: @Bean public OrderService orderService()
   :outertype: OrderApplication

