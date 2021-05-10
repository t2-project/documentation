.. java:import:: java.util ArrayList

.. java:import:: java.util List

.. java:import:: java.util Map

.. java:import:: java.util Optional

.. java:import:: org.slf4j Logger

.. java:import:: org.slf4j LoggerFactory

.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: org.springframework.http ResponseEntity

.. java:import:: org.springframework.web.client RestClientException

.. java:import:: org.springframework.web.client RestTemplate

.. java:import:: com.fasterxml.jackson.core JsonProcessingException

.. java:import:: com.fasterxml.jackson.databind DeserializationFeature

.. java:import:: com.fasterxml.jackson.databind JsonNode

.. java:import:: com.fasterxml.jackson.databind ObjectMapper

.. java:import:: de.unistuttgart.t2.common CartContent

.. java:import:: de.unistuttgart.t2.common Product

.. java:import:: de.unistuttgart.t2.common ReservationRequest

.. java:import:: de.unistuttgart.t2.common.saga SagaRequest

.. java:import:: de.unistuttgart.t2.uibackend.exceptions CartInteractionFailedException

.. java:import:: de.unistuttgart.t2.uibackend.exceptions OrderNotPlacedException

.. java:import:: de.unistuttgart.t2.uibackend.exceptions ReservationFailedException

.. java:import:: io.github.resilience4j.retry Retry

.. java:import:: io.github.resilience4j.retry RetryConfig

.. java:import:: io.github.resilience4j.retry RetryRegistry

UIBackendService
================

.. java:package:: de.unistuttgart.t2.uibackend
   :noindex:

.. java:type:: public class UIBackendService

   Manages interaction with other services.

   :author: maumau

Fields
------
config
^^^^^^

.. java:field::  RetryConfig config
   :outertype: UIBackendService

registry
^^^^^^^^

.. java:field::  RetryRegistry registry
   :outertype: UIBackendService

retry
^^^^^

.. java:field::  Retry retry
   :outertype: UIBackendService

template
^^^^^^^^

.. java:field:: @Autowired  RestTemplate template
   :outertype: UIBackendService

Constructors
------------
UIBackendService
^^^^^^^^^^^^^^^^

.. java:constructor:: public UIBackendService(String cartUrl, String inventoryUrl, String orchestratorUrl, String reservationEndpoint)
   :outertype: UIBackendService

Methods
-------
addItemToCart
^^^^^^^^^^^^^

.. java:method:: public void addItemToCart(String sessionId, String productId, Integer units) throws CartInteractionFailedException
   :outertype: UIBackendService

   Add the given number units of product to a users cart.

   If the product is already in the cart, the units of that product will be updated.

   :param sessionId: identifies the cart to add to
   :param productId: id of product to be added
   :param units: number of units to be added
   :throws CartInteractionFailedException: if the request number of unit could not be placed in the cart.

confirmOrder
^^^^^^^^^^^^

.. java:method:: public void confirmOrder(String sessionId, String cardNumber, String cardOwner, String checksum) throws OrderNotPlacedException
   :outertype: UIBackendService

   Posts a request to start a transaction to the orchestrator.

   :param sessionId: identifies the session
   :param cardNumber: part of payment details
   :param cardOwner: part of payment details
   :param checksum: part of payment details

deleteCart
^^^^^^^^^^

.. java:method:: public void deleteCart(String sessionId) throws CartInteractionFailedException
   :outertype: UIBackendService

   Delete the entire cart for the given sessionId.

   :param sessionId: identifies the cart content to delete
   :throws CartInteractionFailedException: if anything went wrong while talking to the cart

deleteItemFromCart
^^^^^^^^^^^^^^^^^^

.. java:method:: public void deleteItemFromCart(String sessionId, String productId, Integer units) throws CartInteractionFailedException
   :outertype: UIBackendService

   Delete the given number units of product from a users cart.

   If the number of units in the cart decrease to zero or less, the product is remove from the cart. If the no such product is in cart, do nothing.

   :param sessionId: identifies the cart to delete from
   :param productId: id of the product to be deleted
   :param units: number of units to be deleted
   :throws CartInteractionFailedException: if anything went wrong while talking to the cart

getAllProducts
^^^^^^^^^^^^^^

.. java:method:: public List<Product> getAllProducts()
   :outertype: UIBackendService

   Get a list of all products from the inventory.

   TODO : the generated endpoints do things with pages. this gets the first twenty items only.

   :return: a list of all products in the inventory. (might be incomplete)

getCartContent
^^^^^^^^^^^^^^

.. java:method:: protected Optional<CartContent> getCartContent(String sessionId)
   :outertype: UIBackendService

   Get the content of the cart belonging to the given sessionId.

   If there is either no cart content for the given sessionId, or the retrieval of the content failed, an empty optional is returned.

   :param sessionId:
   :return: content of cart iff it exists

getProductsInCart
^^^^^^^^^^^^^^^^^

.. java:method:: public List<Product> getProductsInCart(String sessionId)
   :outertype: UIBackendService

   Get a list of all products in a users cart.

   :param sessionId: identfies the cart content to get
   :return: a list of the product in the cart

getSingleProduct
^^^^^^^^^^^^^^^^

.. java:method:: protected Optional<Product> getSingleProduct(String productId)
   :outertype: UIBackendService

   Get the product with the given productId from the inventory.

   If there is either no product with the given sessionId, or the retrieval of the product failed, an empty optional is returned.

   :param productId: id of the product to be retrieved
   :return: product with given id iff it exists

makeReservations
^^^^^^^^^^^^^^^^

.. java:method:: public Product makeReservations(String sessionId, String productId, Integer units) throws ReservationFailedException
   :outertype: UIBackendService

   Reserve a the given number of units of the given product.

   :param sessionId: identifies the session to reserve for
   :param productId: identifies the product to reserve of
   :param units: number of units to reserve
   :throws ReservationFailedException: if the reservation could not be placed
   :return: the product the reservation was made for

