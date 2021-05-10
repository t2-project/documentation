.. java:import:: org.slf4j Logger

.. java:import:: org.slf4j LoggerFactory

.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: de.unistuttgart.t2.common.saga SagaData

.. java:import:: de.unistuttgart.t2.common.saga.commands ActionCommand

.. java:import:: de.unistuttgart.t2.common.saga.commands CompensationCommand

.. java:import:: de.unistuttgart.t2.common.saga.commands SagaCommand

.. java:import:: de.unistuttgart.t2.inventory InventoryService

.. java:import:: io.eventuate.tram.commands.consumer CommandHandlerReplyBuilder

.. java:import:: io.eventuate.tram.commands.consumer CommandHandlers

.. java:import:: io.eventuate.tram.commands.consumer CommandMessage

.. java:import:: io.eventuate.tram.messaging.common Message

.. java:import:: io.eventuate.tram.sagas.participant SagaCommandHandlersBuilder

InventoryCommandHandler
=======================

.. java:package:: de.unistuttgart.t2.inventory.saga
   :noindex:

.. java:type:: public class InventoryCommandHandler

   handles messages for the inventroy service. listens to the \ ``inventory``\  queue. commits reservations upon receiving a \ :java:ref:`ActionCommand <de.unistuttgart.t2.common.saga.commands.ActionCommand>`\  or deletes reservations without committing them upon receiving a \ :java:ref:`CompensationCommand <de.unistuttgart.t2.common.saga.commands.CompensationCommand>`\ .

   :author: stiesssh

Methods
-------
commandHandlers
^^^^^^^^^^^^^^^

.. java:method:: public CommandHandlers commandHandlers()
   :outertype: InventoryCommandHandler

commitReservation
^^^^^^^^^^^^^^^^^

.. java:method:: public Message commitReservation(CommandMessage<ActionCommand> cm)
   :outertype: InventoryCommandHandler

   commit reservations associated with given sessionId to a products.

   :param cm: message with the command. also holds the session id
   :return: the reply message

undoReservations
^^^^^^^^^^^^^^^^

.. java:method:: public Message undoReservations(CommandMessage<CompensationCommand> cm)
   :outertype: InventoryCommandHandler

   delete reservations associated with given sessionId from products.

   :param cm: message with the command. also holds the session id
   :return: the reply message

