.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: org.springframework.transaction.annotation Transactional

.. java:import:: de.unistuttgart.t2.order.repository OrderItem

.. java:import:: de.unistuttgart.t2.order.repository OrderRepository

.. java:import:: de.unistuttgart.t2.order.repository OrderStatus

OrderService
============

.. java:package:: de.unistuttgart.t2.order
   :noindex:

.. java:type:: @Transactional public class OrderService

   creates and updates orders.

   :author: maumau

Methods
-------
createOrder
^^^^^^^^^^^

.. java:method:: public String createOrder(String sessionId)
   :outertype: OrderService

   create a new Order and save it to the repository. the status of the new order is \ :java:ref:`OrderStatus.SUCCESS`\ .

   :param sessionId: -
   :return: Id of created order

rejectOrder
^^^^^^^^^^^

.. java:method:: public void rejectOrder(String orderId)
   :outertype: OrderService

   Set the state of an order to \ :java:ref:`OrderStatus.FAILURE`\ . If the given id does not match any order nothing happens. This operation is idempotent, as a order may never change from "failure" to any other status.

   :param orderId: - id of order that is to be rejected
   :throws NoSuchElementException: if the id is in the db but retrieval fails anyway.

