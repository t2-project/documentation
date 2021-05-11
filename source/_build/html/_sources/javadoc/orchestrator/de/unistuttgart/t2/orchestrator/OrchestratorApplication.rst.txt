.. java:import:: org.springframework.boot SpringApplication

.. java:import:: org.springframework.boot.autoconfigure EnableAutoConfiguration

.. java:import:: org.springframework.boot.autoconfigure SpringBootApplication

.. java:import:: org.springframework.context.annotation Bean

.. java:import:: org.springframework.context.annotation Import

.. java:import:: de.unistuttgart.t2.orchestrator.saga Saga

.. java:import:: io.eventuate.tram.sagas.orchestration SagaInstanceFactory

.. java:import:: io.eventuate.tram.sagas.spring.orchestration SagaOrchestratorConfiguration

.. java:import:: io.eventuate.tram.spring.consumer.kafka EventuateTramKafkaMessageConsumerConfiguration

.. java:import:: io.eventuate.tram.spring.messaging.producer.jdbc TramMessageProducerJdbcConfiguration

.. java:import:: org.springframework.data.jpa.repository.config EnableJpaRepositories

.. java:import:: io.eventuate.tram.spring.optimisticlocking OptimisticLockingDecoratorConfiguration

OrchestratorApplication
=======================

.. java:package:: de.unistuttgart.t2.orchestrator
   :noindex:

.. java:type:: @SpringBootApplication @EnableJpaRepositories @EnableAutoConfiguration @Import public class OrchestratorApplication

   Orchestrates distributed transactions according to the saga pattern.

   :author: maumau

Methods
-------
createSaga
^^^^^^^^^^

.. java:method:: @Bean public Saga createSaga()
   :outertype: OrchestratorApplication

main
^^^^

.. java:method:: public static void main(String[] args)
   :outertype: OrchestratorApplication

orderService
^^^^^^^^^^^^

.. java:method:: @Bean public OrchestratorService orderService(SagaInstanceFactory sagaInstanceFactory, Saga saga)
   :outertype: OrchestratorApplication

