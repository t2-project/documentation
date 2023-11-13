========================
T2-Modulith Architecture
========================

The T2-Modulith application consists of six modules:

.. image:: ./component-diagram.svg
   :target: ./component-diagram.svg
   :alt: Components Diagram created by Spring Modulith

UI Module
---------

The UI module provides a simple website. It is based on the UI of the original `TeaStore <https://github.com/DescartesResearch/TeaStore>`_ and implemented with JSP.
The UI module communicates with the UI backend module directly by inter-process communication.

UI Backend Module
-----------------

The UI backend module acts as an API gateway and interacts with the cart, inventory and order module.
It provides REST endpoints, but they are not used by the UI.

Order Module
------------

The order module is responsible for saving orders to the database and handling the completion of orders (trigger payment, committing reservations, deleting cart).

Inventory Module
----------------

The inventory module is the inventory of the T2-Project.
It manages the products and reservations.

The products are the teas that the store sells and reservations exist to express that a user plans to buy some units of a product.

Payment Module
--------------

The payment module is responsible for contacting the payment provider.

In a more real situation, a payment service would contact different payment providers, e.g. paypal or a certain credit institute based on which payment method a user chose.
However, here the payment module knows only one payment provider and always contact that one.

The default payment provider is the fake `Credit Institute Service <https://github.com/t2-project/creditinstitute>`_.

Cart Module
-----------

The cart module manages the shopping carts of the T2-Project.
The content of a user's shopping cart is a map of Strings to Integers.
Within the context of the T2-Project it contains which products (identified by their id) and how many units there of a users wants to buy.
