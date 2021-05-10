.. java:import:: java.util Collection

.. java:import:: java.util HashMap

.. java:import:: java.util Map

.. java:import:: com.fasterxml.jackson.annotation JsonCreator

.. java:import:: com.fasterxml.jackson.annotation JsonProperty

CartContent
===========

.. java:package:: de.unistuttgart.t2.common
   :noindex:

.. java:type:: public class CartContent

   content of a users shopping cart to be passed from cart to ui backend to ui and vice versa.

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

.. java:method:: public Collection<String> getProductIds()
   :outertype: CartContent

getUnits
^^^^^^^^

.. java:method:: public Integer getUnits(String productId)
   :outertype: CartContent

   get units of product with given id or zero if product not in the cart

   :param productId:
   :return: units of product with given id

setContent
^^^^^^^^^^

.. java:method:: public void setContent(Map<String, Integer> content)
   :outertype: CartContent

