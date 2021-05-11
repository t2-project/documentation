.. java:import:: org.slf4j Logger

.. java:import:: org.slf4j LoggerFactory

.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: de.unistuttgart.t2.common.saga SagaData

.. java:import:: de.unistuttgart.t2.common.saga.commands ActionCommand

.. java:import:: de.unistuttgart.t2.common.saga.commands SagaCommand

.. java:import:: de.unistuttgart.t2.payment PaymentService

.. java:import:: io.eventuate.tram.commands.consumer CommandHandlerReplyBuilder

.. java:import:: io.eventuate.tram.commands.consumer CommandHandlers

.. java:import:: io.eventuate.tram.commands.consumer CommandMessage

.. java:import:: io.eventuate.tram.messaging.common Message

.. java:import:: io.eventuate.tram.sagas.participant SagaCommandHandlersBuilder

PaymentCommandHandler
=====================

.. java:package:: de.unistuttgart.t2.payment.saga
   :noindex:

.. java:type:: public class PaymentCommandHandler

   handles messages for the payment service. listens to the \ ``payment``\  queue. executes payment upon receiving a \ :java:ref:`ActionCommand <de.unistuttgart.t2.common.saga.commands.ActionCommand>`\  or rejects an does not listen for \ :java:ref:`CompensationCommand <de.unistuttgart.t2.common.saga.commands.CompensationCommand>`\  because the payment service has the pivot transaction (i.e. needs no compensation)

   :author: stiesssh

Methods
-------
commandHandlers
^^^^^^^^^^^^^^^

.. java:method:: public CommandHandlers commandHandlers()
   :outertype: PaymentCommandHandler

doAction
^^^^^^^^

.. java:method:: public Message doAction(CommandMessage<ActionCommand> message)
   :outertype: PaymentCommandHandler

   do some payment.

   :param message: the command
   :return: reply message, either success of failure

