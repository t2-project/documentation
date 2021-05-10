.. java:import:: org.springframework.boot.autoconfigure EnableAutoConfiguration

.. java:import:: org.springframework.context.annotation Bean

.. java:import:: org.springframework.context.annotation Configuration

.. java:import:: org.springframework.context.annotation Import

.. java:import:: org.springframework.context.annotation Profile

.. java:import:: org.springframework.data.jpa.repository.config EnableJpaRepositories

.. java:import:: de.unistuttgart.t2.payment.saga PaymentCommandHandler

.. java:import:: io.eventuate.tram.sagas.participant SagaCommandDispatcher

.. java:import:: io.eventuate.tram.sagas.participant SagaCommandDispatcherFactory

.. java:import:: io.eventuate.tram.sagas.spring.participant SagaParticipantConfiguration

.. java:import:: io.eventuate.tram.spring.consumer.kafka EventuateTramKafkaMessageConsumerConfiguration

.. java:import:: io.eventuate.tram.spring.messaging.producer.jdbc TramMessageProducerJdbcConfiguration

.. java:import:: io.eventuate.tram.spring.optimisticlocking OptimisticLockingDecoratorConfiguration

IncludeSagaConfig
=================

.. java:package:: de.unistuttgart.t2.payment.config
   :noindex:

.. java:type:: @Import @EnableJpaRepositories @EnableAutoConfiguration @Profile @Configuration public class IncludeSagaConfig

   Configuration to run application with saga. Supposed to be used when CDC service is up and running somewhere.

   :author: maumau

Methods
-------
paymentCommandDispatcher
^^^^^^^^^^^^^^^^^^^^^^^^

.. java:method:: @Bean public SagaCommandDispatcher paymentCommandDispatcher(PaymentCommandHandler target, SagaCommandDispatcherFactory sagaCommandDispatcherFactory)
   :outertype: IncludeSagaConfig

paymentCommandHandler
^^^^^^^^^^^^^^^^^^^^^

.. java:method:: @Bean public PaymentCommandHandler paymentCommandHandler()
   :outertype: IncludeSagaConfig

