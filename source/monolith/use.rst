======================
T2-Modulith Usage
======================

You can use the T2-Modulith application either by accessing the UI or by using the HTTP endpoints.

* UI: http://localhost:8081/ui/
* API: http://localhost:8081/swagger-ui/index.html

On how to use the UI see the usage section of the `T2-Project UI repository <https://github.com/t2-project/ui#usage>`_.
How to use the API is described below in the following section `HTTP Endpoints <#http-endpoints>`_.

HTTP Endpoints
--------------

The modules ``cart`` and ``inventory`` provide REST endpoints for their specific domain. The ``UI backend`` module provides REST endpoints that represent the actual functionality of the whole application.
The JSP-specific http endpoints provided by the ``ui`` module are not listed here.

**UI Backend:**

* ``/products`` GET list of all products in the inventory
* ``/cart/{id}`` GET list of all products in cart of a specific session
* ``/cart/{id}`` POST list of products to add/update/delete in/from cart of a specific session
* ``/confirm`` POST to place an order

**Cart:**

* ``/cart/{id}`` GET, PUT, POST or DELETE the cart with sessionId ``id`` (does only manipulate the cart, no reservations are made in the inventory)

**Inventory:**

* ``/inventory/{id}`` : GET, PUT, POST or DELETE the product with productId ``id``
* ``/generate`` : GET to generate new products
* ``/restock`` : GET to restock all items

API Usage Examples
^^^^^^^^^^^^^^^^^^

Base URL: ``http://localhost:8081/``

In the examples we are using ``<productId>`` and ``{sessionId}`` as placeholders. You have to replace them with real values. The session id can be arbitrary string, the product id has to match a product that is actually in your inventory.

Access the products / inventory
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Endpoint to get all products is ``GET /products``\ :

.. code-block:: shell

   curl http://localhost:8081/products

Response:

.. code-block:: json

   [
       {"id":"3a2b20be-2582-47c6-9524-41b5922dbb2c","name":"Earl Grey (loose)","description":"very nice Earl Grey (loose) tea","units":529,"price":2.088258409676226},
   // [...]
       {"id":"89854456-15e0-4ab1-aa0c-aa41915a988c","name":"Sencha (25 bags)","description":"very nice Sencha (25 bags) tea","units":101,"price":0.6923181656954707}
   ]

There are more REST endpoints automatically provided by Spring Data to access inventory items...

An explanatory request to get a specific inventory item with id ``<productId>``\ :

.. code-block:: shell

   curl http://localhost:8081/inventory/<productId>

Response:

.. code-block:: json

   {
     "name" : "Darjeeling (loose)",
     "description" : "very nice Darjeeling (loose) tea",
     "units" : 264,
     "price" : 1.6977123432245298,
     "reservations" : [ ],
     "_links" : {
       "self" : {
         "href" : "http://localhost:8081/inventory/<productId>"
       },
       "inventory" : {
         "href" : "http://localhost:8081/inventory/<productId>"
       }
     }
   }

Restocking the Inventory
~~~~~~~~~~~~~~~~~~~~~~~~

If all items are sold out, this is how you restock all of them.

.. code-block:: shell

   curl http://localhost:8081/restock

If there are no products in the inventory (not as in '0 units of a product' but as in 'there is no product at all'), do this to generate new products.

.. code-block:: shell

   curl http://localhost:8081/generate

Get the products in your cart
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The cart is linked to a session id. 
Request to get the cart for the session id ``{sessionId}``\ :

.. code-block:: shell

   curl http://localhost:8081/cart/{sessionId}

Response if cart is empty:

.. code-block:: json

   []

Response if cart includes one product with 3 units:

.. code-block:: json

   [{"id":"<productId>","name":"Darjeeling (loose)","description":"very nice Darjeeling (loose) tea","units":3,"price":1.6977123432245298}]

Update the cart
~~~~~~~~~~~~~~~

Add product with id ``<productId>`` with 3 units to cart of session with id ``{sessionId}``\ :

.. code-block:: shell

   curl -i -X POST -H "Content-Type:application/json" -d '{"content":{"<productId>":3}}' http://localhost:8081/cart/{sessionId}

Response (successfully added items):

.. code-block:: json

   [{"id":"<productId>","name":"Darjeeling (loose)","description":"very nice Darjeeling (loose) tea","units":3,"price":1.6977123432245298}]

Remove product with id ``<productId>`` from cart of session with id ``{sessionId}``\ :

.. code-block:: shell

   curl -i -X POST -H "Content-Type:application/json" -d '{"content":{"<productId>":-3}}'  http://localhost:8081/cart/{sessionId}

Response:

.. code-block:: json

   []

The response is empty, because it only includes added items, not removed items.

Confirm Order
~~~~~~~~~~~~~

With this, you place an order for the session ``{sessionId}``\ , with the given payment details.

.. code-block:: shell

   curl -i -X POST -H "Content-Type:application/json" -d '{"cardNumber":"num","cardOwner":"own","checksum":"sum", "sessionId":"{sessionId}"}' http://localhost:8081/confirm
