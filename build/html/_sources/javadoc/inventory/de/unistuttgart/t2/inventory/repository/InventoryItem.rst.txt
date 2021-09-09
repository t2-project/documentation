.. java:import:: java.util ArrayList

.. java:import:: java.util List

.. java:import:: javax.persistence CascadeType

.. java:import:: javax.persistence Column

.. java:import:: javax.persistence Entity

.. java:import:: javax.persistence GeneratedValue

.. java:import:: javax.persistence Id

.. java:import:: javax.persistence OneToMany

.. java:import:: javax.persistence Table

.. java:import:: org.hibernate.annotations GenericGenerator

.. java:import:: com.fasterxml.jackson.annotation JsonCreator

.. java:import:: com.fasterxml.jackson.annotation JsonIgnore

.. java:import:: com.fasterxml.jackson.annotation JsonProperty

InventoryItem
=============

.. java:package:: de.unistuttgart.t2.inventory.repository
   :noindex:

.. java:type:: @Entity @Table public class InventoryItem

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

.. java:constructor:: public InventoryItem(String id, String name, String description, int units, double price)
   :outertype: InventoryItem

InventoryItem
^^^^^^^^^^^^^

.. java:constructor:: @JsonCreator public InventoryItem(String id, String name, String description, int units, double price, List<Reservation> reservations)
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

deleteReservation
^^^^^^^^^^^^^^^^^

.. java:method:: public void deleteReservation(String sessionId)
   :outertype: InventoryItem

   :param sessionId:

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

.. java:method:: public List<Reservation> getReservations()
   :outertype: InventoryItem

getUnits
^^^^^^^^

.. java:method:: public int getUnits()
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

