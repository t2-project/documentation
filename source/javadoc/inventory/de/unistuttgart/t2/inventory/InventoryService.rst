.. java:import:: java.util List

.. java:import:: java.util NoSuchElementException

.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: org.springframework.transaction.annotation Transactional

.. java:import:: de.unistuttgart.t2.inventory.repository InventoryItem

.. java:import:: de.unistuttgart.t2.inventory.repository ProductRepository

.. java:import:: de.unistuttgart.t2.inventory.repository Reservation

.. java:import:: de.unistuttgart.t2.inventory.repository ReservationRepository

InventoryService
================

.. java:package:: de.unistuttgart.t2.inventory
   :noindex:

.. java:type:: @Transactional public class InventoryService

   Interactions with the product repository that involve reservations.

   :author: maumau

Constructors
------------
InventoryService
^^^^^^^^^^^^^^^^

.. java:constructor:: public InventoryService(ProductRepository productRepository, ReservationRepository reservationRepository)
   :outertype: InventoryService

Methods
-------
handleSagaAction
^^^^^^^^^^^^^^^^

.. java:method:: public void handleSagaAction(String sessionId)
   :outertype: InventoryService

   commit reservations associated with given sessionId.

   :param sessionId: to identify the reservations to delete

handleSagaCompensation
^^^^^^^^^^^^^^^^^^^^^^

.. java:method:: public void handleSagaCompensation(String sessionId)
   :outertype: InventoryService

   delete reservations of cancelled order from repository.

   :param sessionId: to identify which reservations to delete

makeReservation
^^^^^^^^^^^^^^^

.. java:method:: public InventoryItem makeReservation(String productId, String sessionId, int units) throws NoSuchElementException
   :outertype: InventoryService

   attach a reservation for the given session to the given product.

   :param productId: products to reserve of
   :param sessionId: user to reserve for
   :param units: amount to reserve
   :throws IllegalArgumentException: if any parameter is null
   :throws NoSuchElementException: if the product does not exist

