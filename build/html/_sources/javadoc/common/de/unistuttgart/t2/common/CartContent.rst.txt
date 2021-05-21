.. java:import:: java.util Collection

.. java:import:: java.util HashMap

.. java:import:: java.util Map

.. java:import:: com.fasterxml.jackson.annotation JsonCreator

.. java:import:: com.fasterxml.jackson.annotation JsonIgnore

.. java:import:: com.fasterxml.jackson.annotation JsonProperty

CartContent
===========

.. java:package:: de.unistuttgart.t2.common
   :noindex:

.. java:type:: public class CartContent

   The content of a users shopping cart.

   Holds the productIds of the products in the cart and how many units of each product are in the cart.

   Used to communicated with the cart service.

   :author: maumau

Constructors
------------
CartContent
^^^^^^^^^^^

.. java:constructor:: public CartContent()
   :outertype: CartContent

CartContent
^^^^^^^^^^^

.. java:constructor:: @JsonCreator public CartContent(Map<String, Integer> content)
   :outertype: CartContent

Methods
-------
getContent
^^^^^^^^^^

.. java:method:: public Map<String, Integer> getContent()
   :outertype: CartContent

getProductIds
^^^^^^^^^^^^^

.. java:method:: @JsonIgnore public Collection<String> getProductIds()
   :outertype: CartContent

   Get the productIds of the products in this cart.

   :return: ids of all products in the cart

getUnits
^^^^^^^^

.. java:method:: @JsonIgnore public Integer getUnits(String productId)
   :outertype: CartContent

   Get the number of units of a product with the given id or zero if the product is not in the cart.

   :param productId: to identify the product
   :return: number of units if the product is in the cart, zero otherwise

setContent
^^^^^^^^^^

.. java:method:: public void setContent(Map<String, Integer> content)
   :outertype: CartContent

