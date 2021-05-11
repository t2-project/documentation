.. java:import:: org.springframework.boot.autoconfigure EnableAutoConfiguration

.. java:import:: org.springframework.boot.autoconfigure.jdbc DataSourceAutoConfiguration

.. java:import:: org.springframework.boot.autoconfigure.jdbc DataSourceTransactionManagerAutoConfiguration

.. java:import:: org.springframework.boot.autoconfigure.orm.jpa HibernateJpaAutoConfiguration

.. java:import:: org.springframework.context.annotation Configuration

.. java:import:: org.springframework.context.annotation Profile

.. java:import:: io.eventuate.tram.spring.consumer.jdbc TramConsumerJdbcAutoConfiguration

.. java:import:: io.eventuate.tram.spring.messaging.common TramMessagingCommonAutoConfiguration

ExcludeSagaConfig
=================

.. java:package:: de.unistuttgart.t2.payment.config
   :noindex:

.. java:type:: @EnableAutoConfiguration @Profile @Configuration public class ExcludeSagaConfig

   Configuration that excludes saga related things. Supposed to be use in case i want to run the payment without the other components. Tram* are from the actual saga and Data* and Hibernate are from the db, that the CDC needs.

   :author: maumau

