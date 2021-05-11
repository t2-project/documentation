.. java:import:: java.time Instant

.. java:import:: java.util Date

.. java:import:: org.springframework.data.annotation Id

OrderItem
=========

.. java:package:: de.unistuttgart.t2.order.repository
   :noindex:

.. java:type:: public class OrderItem

   represents an order. each oder has a unique orderId to find it in the repository, a sessionId to correlate it to other things and a timestamp because of reasons.

   :author: sarah sophie stieß

Constructors
------------
OrderItem
^^^^^^^^^

.. java:constructor:: public OrderItem()
   :outertype: OrderItem

   used (and required) by repository template

OrderItem
^^^^^^^^^

.. java:constructor:: public OrderItem(String sessionId)
   :outertype: OrderItem

   create a new order there is no \ ``orderId``\  because it gets set by repository. \ ``status``\  of a new order is always \ :java:ref:`OrderStatus.SUCCESS`\ , \ ``timestamp``\  is always the current time.

   :param sessionId:

Methods
-------
getOrderId
^^^^^^^^^^

.. java:method:: public String getOrderId()
   :outertype: OrderItem

getSessionId
^^^^^^^^^^^^

.. java:method:: public String getSessionId()
   :outertype: OrderItem

getStatus
^^^^^^^^^

.. java:method:: public OrderStatus getStatus()
   :outertype: OrderItem

getTimestamp
^^^^^^^^^^^^

.. java:method:: public Date getTimestamp()
   :outertype: OrderItem

setOrderId
^^^^^^^^^^

.. java:method:: public void setOrderId(String orderId)
   :outertype: OrderItem

setSessionId
^^^^^^^^^^^^

.. java:method:: public void setSessionId(String sessionId)
   :outertype: OrderItem

setStatus
^^^^^^^^^

.. java:method:: public void setStatus(OrderStatus status)
   :outertype: OrderItem

setTimestamp
^^^^^^^^^^^^

.. java:method:: public void setTimestamp(Date timestamp)
   :outertype: OrderItem

toString
^^^^^^^^

.. java:method:: @Override public String toString()
   :outertype: OrderItem

