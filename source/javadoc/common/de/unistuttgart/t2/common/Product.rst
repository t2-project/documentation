.. java:import:: com.fasterxml.jackson.annotation JsonCreator

.. java:import:: com.fasterxml.jackson.annotation JsonProperty

Product
=======

.. java:package:: de.unistuttgart.t2.common
   :noindex:

.. java:type:: public class Product

   a product as sold by the store. to be passed from inventory to ui backend.

   :author: maumau

Constructors
------------
Product
^^^^^^^

.. java:constructor:: public Product()
   :outertype: Product

Product
^^^^^^^

.. java:constructor:: @JsonCreator public Product(String id, String name, String desription, int units, double price)
   :outertype: Product

Product
^^^^^^^

.. java:constructor:: public Product(String name, String desription, int units, double price)
   :outertype: Product

Methods
-------
getDescription
^^^^^^^^^^^^^^

.. java:method:: public String getDescription()
   :outertype: Product

getId
^^^^^

.. java:method:: public String getId()
   :outertype: Product

getName
^^^^^^^

.. java:method:: public String getName()
   :outertype: Product

getPrice
^^^^^^^^

.. java:method:: public double getPrice()
   :outertype: Product

getUnits
^^^^^^^^

.. java:method:: public int getUnits()
   :outertype: Product

setDescription
^^^^^^^^^^^^^^

.. java:method:: public void setDescription(String desription)
   :outertype: Product

setId
^^^^^

.. java:method:: public void setId(String id)
   :outertype: Product

setName
^^^^^^^

.. java:method:: public void setName(String name)
   :outertype: Product

setPrice
^^^^^^^^

.. java:method:: public void setPrice(double price)
   :outertype: Product

setUnits
^^^^^^^^

.. java:method:: public void setUnits(int units)
   :outertype: Product

