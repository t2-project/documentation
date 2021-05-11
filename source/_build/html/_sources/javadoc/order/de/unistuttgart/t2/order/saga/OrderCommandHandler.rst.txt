.. java:import:: org.slf4j Logger

.. java:import:: org.slf4j LoggerFactory

.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: de.unistuttgart.t2.common.saga OrderCreatedReply

.. java:import:: de.unistuttgart.t2.common.saga SagaData

.. java:import:: de.unistuttgart.t2.common.saga.commands ActionCommand

.. java:import:: de.unistuttgart.t2.common.saga.commands CompensationCommand

.. java:import:: de.unistuttgart.t2.common.saga.commands SagaCommand

.. java:import:: de.unistuttgart.t2.order OrderService

.. java:import:: io.eventuate.tram.commands.consumer CommandHandlerReplyBuilder

.. java:import:: io.eventuate.tram.commands.consumer CommandHandlers

.. java:import:: io.eventuate.tram.commands.consumer CommandMessage

.. java:import:: io.eventuate.tram.messaging.common Message

.. java:import:: io.eventuate.tram.sagas.participant SagaCommandHandlersBuilder

OrderCommandHandler
===================

.. java:package:: de.unistuttgart.t2.order.saga
   :noindex:

.. java:type:: public class OrderCommandHandler

   handles messages for the order service. listens to the \ ``order``\  queue. creates a new order upon receiving a \ :java:ref:`ActionCommand <de.unistuttgart.t2.common.saga.commands.ActionCommand>`\  or rejects an existing order upon receiving a \ :java:ref:`CompensationCommand <de.unistuttgart.t2.common.saga.commands.CompensationCommand>`\ .

   :author: sarah sophie stieß

Methods
-------
commandHandlers
^^^^^^^^^^^^^^^

.. java:method:: public CommandHandlers commandHandlers()
   :outertype: OrderCommandHandler

createOrder
^^^^^^^^^^^

.. java:method:: public Message createOrder(CommandMessage<ActionCommand> cm)
   :outertype: OrderCommandHandler

   create a new order.

   :param cm: - the command message
   :return: the reply message. if successful it contains the id of the created order.

rejectOrder
^^^^^^^^^^^

.. java:method:: public Message rejectOrder(CommandMessage<CompensationCommand> cm)
   :outertype: OrderCommandHandler

   reject an existing order.

   :param cm: - the command message
   :return: the reply message

