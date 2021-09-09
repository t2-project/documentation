.. java:import:: java.time Instant

.. java:import:: java.util Date

.. java:import:: javax.persistence Column

.. java:import:: javax.persistence Entity

.. java:import:: javax.persistence FetchType

.. java:import:: javax.persistence GeneratedValue

.. java:import:: javax.persistence Id

.. java:import:: javax.persistence ManyToOne

.. java:import:: javax.persistence Table

.. java:import:: javax.persistence Temporal

.. java:import:: javax.persistence TemporalType

Reservation
===========

.. java:package:: de.unistuttgart.t2.inventory.repository
   :noindex:

.. java:type:: @Entity @Table public class Reservation

   A Reservation of a certain number of units.

   Reservations have a \ ``creationDate``\  such that they might be killed after they exceeded their time to life.

   :author: maumau

Fields
------
item
^^^^

.. java:field:: @ManyToOne public InventoryItem item
   :outertype: Reservation

Constructors
------------
Reservation
^^^^^^^^^^^

.. java:constructor:: public Reservation()
   :outertype: Reservation

Reservation
^^^^^^^^^^^

.. java:constructor:: public Reservation(int units, String userId, InventoryItem item)
   :outertype: Reservation

Reservation
^^^^^^^^^^^

.. java:constructor:: protected Reservation(int units, Date date, String userId, InventoryItem item)
   :outertype: Reservation

Methods
-------
equals
^^^^^^

.. java:method:: @Override public boolean equals(Object o)
   :outertype: Reservation

getCreationDate
^^^^^^^^^^^^^^^

.. java:method:: public Date getCreationDate()
   :outertype: Reservation

getId
^^^^^

.. java:method:: public int getId()
   :outertype: Reservation

getUnits
^^^^^^^^

.. java:method:: public int getUnits()
   :outertype: Reservation

getUserId
^^^^^^^^^

.. java:method:: public String getUserId()
   :outertype: Reservation

toString
^^^^^^^^

.. java:method:: @Override public String toString()
   :outertype: Reservation

updateUnits
^^^^^^^^^^^

.. java:method:: public void updateUnits(int update)
   :outertype: Reservation

   increase number of units by 'update' and also renew the creation date.

   :param update: additionally reserved units

