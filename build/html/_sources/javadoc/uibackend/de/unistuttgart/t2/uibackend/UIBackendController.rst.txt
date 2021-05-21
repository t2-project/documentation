.. java:import:: java.util ArrayList

.. java:import:: java.util List

.. java:import:: java.util Map.Entry

.. java:import:: javax.servlet.http HttpSession

.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: org.springframework.http HttpHeaders

.. java:import:: org.springframework.http HttpStatus

.. java:import:: org.springframework.http ResponseEntity

.. java:import:: org.springframework.web.bind.annotation ExceptionHandler

.. java:import:: org.springframework.web.bind.annotation GetMapping

.. java:import:: org.springframework.web.bind.annotation PostMapping

.. java:import:: org.springframework.web.bind.annotation RequestBody

.. java:import:: org.springframework.web.bind.annotation RequestHeader

.. java:import:: org.springframework.web.bind.annotation ResponseStatus

.. java:import:: org.springframework.web.bind.annotation RestController

.. java:import:: de.unistuttgart.t2.common CartContent

.. java:import:: de.unistuttgart.t2.common OrderRequest

.. java:import:: de.unistuttgart.t2.common Product

.. java:import:: de.unistuttgart.t2.uibackend.exceptions CartInteractionFailedException

.. java:import:: de.unistuttgart.t2.uibackend.exceptions OrderNotPlacedException

.. java:import:: de.unistuttgart.t2.uibackend.exceptions ReservationFailedException

UIBackendController
===================

.. java:package:: de.unistuttgart.t2.uibackend
   :noindex:

.. java:type:: @RestController public class UIBackendController

   Defines the http enpoints of the UIBackend.

   :author: maumau

Methods
-------
addItemsToCart
^^^^^^^^^^^^^^

.. java:method:: @PostMapping public List<Product> addItemsToCart(String sessionId, CartContent products) throws ReservationFailedException, CartInteractionFailedException
   :outertype: UIBackendController

   Add units of the given products to the cart.

   Only add the products to the cart if the requested number of unit is available. To achieve this, at first a reservations are placed in the inventory and only after the reservations are succeeded be are the products added to the cart.

   Replies as long as at least on product is added to the cart.

   :param sessionId: sessionId of user
   :param products: products to be added, including the number of units thereof
   :throws ReservationFailedException: if all reservations failed.
   :return: a list of all products that were added with \ ``units``\  being the number of unit that were added / reserved.

confirmOrder
^^^^^^^^^^^^

.. java:method:: @PostMapping public void confirmOrder(String sessionId, OrderRequest request) throws OrderNotPlacedException, CartInteractionFailedException
   :outertype: UIBackendController

   place an order, i.e. start a transaction. upon successfully placing the order the cart is cleared and the session gets invalidated. if the user wants to place another order he needs a new http session.

   :param sessionId: sessionId of user
   :param request: payment details
   :throws OrderNotPlacedException: if the order could not be placed.

deleteItemsFromCart
^^^^^^^^^^^^^^^^^^^

.. java:method:: @PostMapping public void deleteItemsFromCart(String sessionId, CartContent products)
   :outertype: UIBackendController

   Delete a product from the cart.

   :param sessionId: sessionId of user
   :param products: products products to be deleted, including the number of units

getAllProducts
^^^^^^^^^^^^^^

.. java:method:: @GetMapping public List<Product> getAllProducts(HttpSession session)
   :outertype: UIBackendController

   Get a list of all products in the inventory. The session exists such that i can get a cookie even though i am not using the ui (frontend), e.g. as the load generator does.

   :param session: http session
   :return: a list of all product in the inventory.

getCart
^^^^^^^

.. java:method:: @GetMapping public List<Product> getCart(String sessionId)
   :outertype: UIBackendController

   Get a list of all products in users cart.

   :param sessionId: sessionId of user
   :return: a list of all products in the users cart.

greetingsWithHeaders
^^^^^^^^^^^^^^^^^^^^

.. java:method:: @GetMapping public String greetingsWithHeaders(String sessionId)
   :outertype: UIBackendController

   Greets in a friendly manner.

   :return: a friendly greeting

handleCartInteractionFailedException
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. java:method:: @ExceptionHandler @ResponseStatus public ResponseEntity<String> handleCartInteractionFailedException(CartInteractionFailedException exception)
   :outertype: UIBackendController

   Creates the response entity if a request could not be served because the interaction with the cart service failed.

   :param exception:
   :return: a response entity with an exceptional message

handleOrderNotPlacesException
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. java:method:: @ExceptionHandler @ResponseStatus public ResponseEntity<String> handleOrderNotPlacesException(OrderNotPlacedException exception)
   :outertype: UIBackendController

   Creates the response entity if a request could not be served because placing an order failed.

   :param exception:
   :return: a response entity with an exceptional message

handleReservationFailedException
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. java:method:: @ExceptionHandler @ResponseStatus public ResponseEntity<String> handleReservationFailedException(ReservationFailedException exception)
   :outertype: UIBackendController

   Creates the response entity if a request could not be served because of a failed reservation.

   :param exception:
   :return: a response entity with an exceptional message

