.. java:import:: de.unistuttgart.t2.common.saga SagaData

.. java:import:: io.eventuate.tram.commands.common Command

SagaCommand
===========

.. java:package:: de.unistuttgart.t2.common.saga.commands
   :noindex:

.. java:type:: public abstract class SagaCommand implements Command

   generic command to saga participants. storing the names of the channels here is not intended, but i do it anyway because i want them at one central place.

   :author: maumau

Fields
------
inventory
^^^^^^^^^

.. java:field:: public static final String inventory
   :outertype: SagaCommand

order
^^^^^

.. java:field:: public static final String order
   :outertype: SagaCommand

payment
^^^^^^^

.. java:field:: public static final String payment
   :outertype: SagaCommand

Constructors
------------
SagaCommand
^^^^^^^^^^^

.. java:constructor:: public SagaCommand(SagaData data)
   :outertype: SagaCommand

SagaCommand
^^^^^^^^^^^

.. java:constructor:: public SagaCommand()
   :outertype: SagaCommand

Methods
-------
getData
^^^^^^^

.. java:method:: public SagaData getData()
   :outertype: SagaCommand

setData
^^^^^^^

.. java:method:: public void setData(SagaData data)
   :outertype: SagaCommand

