.. java:import:: org.springframework.boot SpringApplication

.. java:import:: org.springframework.boot.autoconfigure SpringBootApplication

.. java:import:: org.springframework.context.annotation Bean

.. java:import:: org.springframework.context.annotation Import

.. java:import:: org.springframework.data.mongodb.repository.config EnableMongoRepositories

.. java:import:: org.springframework.scheduling.concurrent ThreadPoolTaskScheduler

.. java:import:: de.unistuttgart.t2.inventory.config ExculdeSagaConfig

.. java:import:: de.unistuttgart.t2.inventory.config IncludeSagaConfig

.. java:import:: de.unistuttgart.t2.inventory.repository ProductRepository

.. java:import:: de.unistuttgart.t2.inventory.repository TimeoutCollector

InventoryApplication
====================

.. java:package:: de.unistuttgart.t2.inventory
   :noindex:

.. java:type:: @Import @EnableMongoRepositories @SpringBootApplication public class InventoryApplication

Methods
-------
inventoryService
^^^^^^^^^^^^^^^^

.. java:method:: @Bean public InventoryService inventoryService()
   :outertype: InventoryApplication

main
^^^^

.. java:method:: public static void main(String[] args)
   :outertype: InventoryApplication

