.. java:import:: org.springframework.boot.autoconfigure EnableAutoConfiguration

.. java:import:: org.springframework.context.annotation Bean

.. java:import:: org.springframework.context.annotation Configuration

.. java:import:: org.springframework.context.annotation Import

.. java:import:: org.springframework.context.annotation Profile

.. java:import:: org.springframework.data.jpa.repository.config EnableJpaRepositories

.. java:import:: org.springframework.scheduling.concurrent ThreadPoolTaskScheduler

.. java:import:: de.unistuttgart.t2.inventory.repository TimeoutCollector

.. java:import:: de.unistuttgart.t2.inventory.saga InventoryCommandHandler

.. java:import:: io.eventuate.tram.sagas.participant SagaCommandDispatcher

.. java:import:: io.eventuate.tram.sagas.participant SagaCommandDispatcherFactory

.. java:import:: io.eventuate.tram.sagas.spring.participant SagaParticipantConfiguration

.. java:import:: io.eventuate.tram.spring.consumer.kafka EventuateTramKafkaMessageConsumerConfiguration

.. java:import:: io.eventuate.tram.spring.messaging.producer.jdbc TramMessageProducerJdbcConfiguration

TimeoutCollectorConfig
======================

.. java:package:: de.unistuttgart.t2.inventory.config
   :noindex:

.. java:type:: @EnableAutoConfiguration @Profile @Configuration public class TimeoutCollectorConfig

   Configuration to have all beans required for the \ :java:ref:`TimeoutCollector <TimeoutCollector>`\ .

   :author: maumau

Methods
-------
collector
^^^^^^^^^

.. java:method:: @Bean public TimeoutCollector collector()
   :outertype: TimeoutCollectorConfig

threadPoolTaskScheduler
^^^^^^^^^^^^^^^^^^^^^^^

.. java:method:: @Bean public ThreadPoolTaskScheduler threadPoolTaskScheduler()
   :outertype: TimeoutCollectorConfig

