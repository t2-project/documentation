.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: org.springframework.web.bind.annotation GetMapping

.. java:import:: org.springframework.web.bind.annotation PostMapping

.. java:import:: org.springframework.web.bind.annotation RequestBody

.. java:import:: org.springframework.web.bind.annotation RestController

.. java:import:: de.unistuttgart.t2.common Product

.. java:import:: de.unistuttgart.t2.common ReservationRequest

.. java:import:: de.unistuttgart.t2.inventory.repository DataGenerator

.. java:import:: de.unistuttgart.t2.inventory.repository InventoryItem

InventoryController
===================

.. java:package:: de.unistuttgart.t2.inventory
   :noindex:

.. java:type:: @RestController public class InventoryController

   Defines additional endpoints for the inventory. Other endpoints are auto generated.

   :author: maumau

Constructors
------------
InventoryController
^^^^^^^^^^^^^^^^^^^

.. java:constructor:: public InventoryController(InventoryService inventoryService, DataGenerator generator)
   :outertype: InventoryController

Methods
-------
addReservation
^^^^^^^^^^^^^^

.. java:method:: @PostMapping public Product addReservation(ReservationRequest body)
   :outertype: InventoryController

   add a reservation to a product.

   :param body: request body
   :return: the product that the reservation was added to.

generateData
^^^^^^^^^^^^

.. java:method:: @GetMapping public void generateData()
   :outertype: InventoryController

   trigger generation of new products

restock
^^^^^^^

.. java:method:: @GetMapping public void restock()
   :outertype: InventoryController

   trigger restock of all products

