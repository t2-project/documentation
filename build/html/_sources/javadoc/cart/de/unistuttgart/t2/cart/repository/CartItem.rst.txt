.. java:import:: java.time Instant

.. java:import:: java.util Date

.. java:import:: java.util HashMap

.. java:import:: java.util Map

.. java:import:: org.springframework.data.annotation Id

CartItem
========

.. java:package:: de.unistuttgart.t2.cart.repository
   :noindex:

.. java:type:: public class CartItem

   The content of someones cart.

   Cart items have a \ ``creationDate``\  such that they might be killed after they exceeded their time to life.

   :author: maumau

Constructors
------------
CartItem
^^^^^^^^

.. java:constructor:: public CartItem(String id, Map<String, Integer> content, Date creationDate)
   :outertype: CartItem

CartItem
^^^^^^^^

.. java:constructor:: public CartItem(String id, Map<String, Integer> content)
   :outertype: CartItem

CartItem
^^^^^^^^

.. java:constructor:: public CartItem(String id)
   :outertype: CartItem

CartItem
^^^^^^^^

.. java:constructor:: public CartItem()
   :outertype: CartItem

Methods
-------
getContent
^^^^^^^^^^

.. java:method:: public Map<String, Integer> getContent()
   :outertype: CartItem

getCreationDate
^^^^^^^^^^^^^^^

.. java:method:: public Date getCreationDate()
   :outertype: CartItem

getId
^^^^^

.. java:method:: public String getId()
   :outertype: CartItem

setContent
^^^^^^^^^^

.. java:method:: public void setContent(Map<String, Integer> content)
   :outertype: CartItem

setCreationDate
^^^^^^^^^^^^^^^

.. java:method:: public void setCreationDate(Date creationDate)
   :outertype: CartItem

setId
^^^^^

.. java:method:: public void setId(String id)
   :outertype: CartItem

