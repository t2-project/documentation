.. java:import:: java.time Instant

.. java:import:: java.util Date

Reservation
===========

.. java:package:: de.unistuttgart.t2.inventory.repository
   :noindex:

.. java:type:: public class Reservation

   A Reservation of a certain number of units. Reservations have a \ ``creationDate``\  such that they might be killed after they exceeded their time to life.

   :author: maumau

Constructors
------------
Reservation
^^^^^^^^^^^

.. java:constructor:: public Reservation()
   :outertype: Reservation

Reservation
^^^^^^^^^^^

.. java:constructor:: public Reservation(int units)
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

getUnits
^^^^^^^^

.. java:method:: public int getUnits()
   :outertype: Reservation

setCreationDate
^^^^^^^^^^^^^^^

.. java:method:: public void setCreationDate(Date creationDate)
   :outertype: Reservation

setUnits
^^^^^^^^

.. java:method:: public void setUnits(int units)
   :outertype: Reservation

   set number of units and also renew the creation date.

   :param units: new number of reserved units

