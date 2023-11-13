.. _monolith:

===================
T2-Modulith
===================

The T2-Modulith is an implementation of the :ref:`T2-Project microservices variant <microservices>` as a monolith.
It has still a modular structure enforced by `Spring Modulith <https://spring.io/projects/spring-modulith>`_. Therefore we name it *T2-Modulith*.

See page :doc:`Architecture <arch>` for more information about the monolithic architecture.
See pages :doc:`Usage <use>` and :doc:`Deployment <deploy>` for more information about how to use the T2-Modulith.


Migration
---------

The following table shows the differences between the microservices and the monolith implementation.

.. list-table::
   :header-rows: 1

   * - Microservice
     - Monolith
     - Comments
   * - `Cart <https://github.com/t2-project/cart>`_
     - Cart Module
     - 
   * - `Inventory <https://github.com/t2-project/inventory>`_
     - Inventory Module
     - 
   * - `Order <https://github.com/t2-project/order>`_
     - Order Module
     - 
   * - `Payment <https://github.com/t2-project/payment>`_
     - Payment Module
     - 
   * - `UI <https://github.com/t2-project/ui>`_
     - UI Module
     - JSP 😕
   * - `UI Backend <https://github.com/t2-project/uibackend>`_
     - UI Backend Module
     - | Still an API gateway for the UI but in a different way:
       | UI interacts with UI Backend via inter-process communication instead of HTTP requests over the network
   * - `Orchestrator <https://github.com/t2-project/orchestrator>`_
     - ❌
     - | Saga Pattern not needed anymore
       | → Simple transaction is used to finalize an order, part of the order module


The `common <https://github.com/t2-project/common>`_ package that is used as a jar file by all microservices for inter-service communication is not used anymore. Some parts are moved to the respective domain-specific module. There is now a ``config`` package that includes the configuration that is relevant for multiple modules, however, without any class definitions required used for communication.


Technical Notes
---------------

* The application gets packaged as a war and not as jar, because of the limitations of JSP used for the UI (see Spring Docs about `JSP Limitations <https://docs.spring.io/spring-boot/docs/current/reference/html/web.html#web.servlet.embedded-container.jsp-limitations>`_\ )
* Default port is set to 8081 to have the same base URL than the `T2-Project UI Backend Service <https://github.com/t2-project/uibackend>`_
