.. java:import:: org.junit.jupiter.api BeforeEach

.. java:import:: org.junit.jupiter.api Test

.. java:import:: org.junit.jupiter.api.extension ExtendWith

.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: org.springframework.boot.test.autoconfigure.data.mongo DataMongoTest

.. java:import:: org.springframework.test.context ActiveProfiles

.. java:import:: org.springframework.test.context ContextConfiguration

.. java:import:: org.springframework.test.context.junit.jupiter SpringExtension

.. java:import:: de.unistuttgart.t2.order.repository OrderItem

.. java:import:: de.unistuttgart.t2.order.repository OrderRepository

.. java:import:: de.unistuttgart.t2.order.repository OrderStatus

OrderTest
=========

.. java:package:: de.unistuttgart.t2.order
   :noindex:

.. java:type:: @DataMongoTest @ExtendWith @ContextConfiguration @ActiveProfiles public class OrderTest

Fields
------
orderRepository
^^^^^^^^^^^^^^^

.. java:field:: @Autowired  OrderRepository orderRepository
   :outertype: OrderTest

orderid
^^^^^^^

.. java:field::  String orderid
   :outertype: OrderTest

Methods
-------
setup
^^^^^

.. java:method:: @BeforeEach public void setup()
   :outertype: OrderTest

testCreateOrder
^^^^^^^^^^^^^^^

.. java:method:: @Test public void testCreateOrder()
   :outertype: OrderTest

testRejectOrder
^^^^^^^^^^^^^^^

.. java:method:: @Test public void testRejectOrder()
   :outertype: OrderTest

