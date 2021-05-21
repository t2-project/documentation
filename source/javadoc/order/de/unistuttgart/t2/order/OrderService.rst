.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: de.unistuttgart.t2.order.repository OrderItem

.. java:import:: de.unistuttgart.t2.order.repository OrderRepository

.. java:import:: de.unistuttgart.t2.order.repository OrderStatus

OrderService
============

.. java:package:: de.unistuttgart.t2.order
   :noindex:

.. java:type:: public class OrderService

   creates and updates orders.

   :author: maumau

Methods
-------
createOrder
^^^^^^^^^^^

.. java:method:: public String createOrder(String sessionId)
   :outertype: OrderService

   create a new Order and save it to the repository. the status of the new order is \ :java:ref:`SUCCESS <OrderStatus.SUCCESS>`\ .

   :param sessionId: id of session to create order for
   :return: orderId of created order

rejectOrder
^^^^^^^^^^^

.. java:method:: public void rejectOrder(String orderId)
   :outertype: OrderService

   Set the state of an order to \ :java:ref:`FAILURE <OrderStatus.FAILURE>`\ . This operation is idempotent, as a order may never change from \ :java:ref:`FAILURE <OrderStatus.FAILURE>`\  to any other status.

   :param orderId: id of order that is to be rejected
   :throws NoSuchElementException: if the id is in the db but retrieval fails anyway.

