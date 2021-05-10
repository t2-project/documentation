.. java:import:: java.util List

.. java:import:: java.util Random

.. java:import:: javax.annotation PostConstruct

.. java:import:: org.slf4j Logger

.. java:import:: org.slf4j LoggerFactory

.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: org.springframework.beans.factory.annotation Value

.. java:import:: org.springframework.stereotype Component

.. java:import:: org.springframework.transaction.annotation Transactional

.. java:import:: org.springframework.web.client RestTemplate

.. java:import:: de.unistuttgart.t2.common CartContent

DataGenerator
=============

.. java:package:: de.unistuttgart.t2.inventory.repository
   :noindex:

.. java:type:: @Component public class DataGenerator

   Generates new products into the product repository or or restocks existing ones. Generation is always triggered after initialisation.

   :author: maumau

Fields
------
inventorySize
^^^^^^^^^^^^^

.. java:field:: @Value protected int inventorySize
   :outertype: DataGenerator

repository
^^^^^^^^^^

.. java:field:: @Autowired  ProductRepository repository
   :outertype: DataGenerator

template
^^^^^^^^

.. java:field::  RestTemplate template
   :outertype: DataGenerator

Methods
-------
generateProducts
^^^^^^^^^^^^^^^^

.. java:method:: @PostConstruct public void generateProducts()
   :outertype: DataGenerator

   Generates products into the product repository. Also generates cart content and reservations, if the cart service is available.

restockProducts
^^^^^^^^^^^^^^^

.. java:method:: @Transactional public void restockProducts()
   :outertype: DataGenerator

   restock products in the repository. at some point all products will be sold out. thus there must be an option the restock them.

