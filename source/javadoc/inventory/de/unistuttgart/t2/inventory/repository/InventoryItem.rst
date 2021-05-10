.. java:import:: java.util HashMap

.. java:import:: java.util Map

.. java:import:: org.springframework.data.annotation Id

.. java:import:: com.fasterxml.jackson.annotation JsonCreator

.. java:import:: com.fasterxml.jackson.annotation JsonIgnore

.. java:import:: com.fasterxml.jackson.annotation JsonProperty

InventoryItem
=============

.. java:package:: de.unistuttgart.t2.inventory.repository
   :noindex:

.. java:type:: public class InventoryItem

   A Product in the inventory. Each product has some describing attributes such as a name, a description and a price, as well as the number of units in stock. If a user placed units of product in their cart, that product has some reservations attached. The actual number of unit in stock shall only ever be changed by committing reservations (c.f. \ :java:ref:`InventoryItem.commitReservation(String)`\ })

   :author: maumau

Constructors
------------
InventoryItem
^^^^^^^^^^^^^

.. java:constructor:: public InventoryItem()
   :outertype: InventoryItem

   because spring framework wants this.

InventoryItem
^^^^^^^^^^^^^

.. java:constructor:: @JsonCreator public InventoryItem(String id, String name, String description, int units, double price)
   :outertype: InventoryItem

InventoryItem
^^^^^^^^^^^^^

.. java:constructor:: public InventoryItem(String id, String name, String description, int units, double price, Map<String, Reservation> reservations)
   :outertype: InventoryItem

Methods
-------
addReservation
^^^^^^^^^^^^^^

.. java:method:: public void addReservation(String sessionId, int unitsToReserve)
   :outertype: InventoryItem

   Add to or updated the products reservations. If a reservation for the given \ ``sessionId``\  already exists, the existing reservation is updated, otherwise a new reservation is added. However, a reservation is only added or updated reservations if enough products are available.

   :param sessionId: to identify user
   :param unitsToReserve: number of units to reserve
   :throws IllegalArgumentException: if not enough units available or otherwise illegal arguments

commitReservation
^^^^^^^^^^^^^^^^^

.. java:method:: public void commitReservation(String sessionId)
   :outertype: InventoryItem

   remove a reservation and decrease units in stock. always use this operation to decrease the the number of unit in stock.

   :param sessionId: to identify the reservation to be committed

equals
^^^^^^

.. java:method:: @Override public boolean equals(Object o)
   :outertype: InventoryItem

getAvailableUnits
^^^^^^^^^^^^^^^^^

.. java:method:: @JsonIgnore public int getAvailableUnits()
   :outertype: InventoryItem

   Calculate the number of available units. The number of available units is \ ``units in stock - sum of reserved units``\

   :throws IllegalStateException: if the reservations are too much.
   :return: number of not yet reserved units of this product

getDescription
^^^^^^^^^^^^^^

.. java:method:: public String getDescription()
   :outertype: InventoryItem

getId
^^^^^

.. java:method:: public String getId()
   :outertype: InventoryItem

getName
^^^^^^^

.. java:method:: public String getName()
   :outertype: InventoryItem

getPrice
^^^^^^^^

.. java:method:: public double getPrice()
   :outertype: InventoryItem

getReservations
^^^^^^^^^^^^^^^

.. java:method:: public Map<String, Reservation> getReservations()
   :outertype: InventoryItem

getUnits
^^^^^^^^

.. java:method:: public int getUnits()
   :outertype: InventoryItem

setDescription
^^^^^^^^^^^^^^

.. java:method:: public void setDescription(String description)
   :outertype: InventoryItem

setId
^^^^^

.. java:method:: public void setId(String id)
   :outertype: InventoryItem

setName
^^^^^^^

.. java:method:: public void setName(String name)
   :outertype: InventoryItem

setPrice
^^^^^^^^

.. java:method:: public void setPrice(double price)
   :outertype: InventoryItem

setReservations
^^^^^^^^^^^^^^^

.. java:method:: public void setReservations(Map<String, Reservation> reservations)
   :outertype: InventoryItem

setUnits
^^^^^^^^

.. java:method:: public void setUnits(int units)
   :outertype: InventoryItem

   set the units. cannot be used to decrease the number of units.

   :param units: new number of unit in stock

toString
^^^^^^^^

.. java:method:: @Override public String toString()
   :outertype: InventoryItem

