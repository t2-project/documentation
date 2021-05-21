.. java:import:: java.net URI

.. java:import:: java.util List

.. java:import:: java.util Map

.. java:import:: javax.servlet.http HttpSession

.. java:import:: org.slf4j Logger

.. java:import:: org.slf4j LoggerFactory

.. java:import:: org.springframework.beans.factory.annotation Autowired

.. java:import:: org.springframework.beans.factory.annotation Value

.. java:import:: org.springframework.core ParameterizedTypeReference

.. java:import:: org.springframework.http HttpEntity

.. java:import:: org.springframework.http HttpHeaders

.. java:import:: org.springframework.http HttpMethod

.. java:import:: org.springframework.http RequestEntity

.. java:import:: org.springframework.http ResponseEntity

.. java:import:: org.springframework.stereotype Controller

.. java:import:: org.springframework.ui Model

.. java:import:: org.springframework.web.bind.annotation GetMapping

.. java:import:: org.springframework.web.bind.annotation ModelAttribute

.. java:import:: org.springframework.web.bind.annotation PostMapping

.. java:import:: org.springframework.web.client RestTemplate

.. java:import:: org.springframework.web.servlet.mvc.support RedirectAttributes

.. java:import:: org.springframework.web.servlet.view RedirectView

.. java:import:: de.unistuttgart.t2.common CartContent

.. java:import:: de.unistuttgart.t2.common OrderRequest

.. java:import:: de.unistuttgart.t2.common Product

.. java:import:: de.unistuttgart.t2.ui.domain ItemToAdd

.. java:import:: de.unistuttgart.t2.ui.domain PaymentDetails

UIController
============

.. java:package:: de.unistuttgart.t2.ui
   :noindex:

.. java:type:: @Controller public class UIController

   Defines the http enpoints of the UI.

   :author: maumau

Constructors
------------
UIController
^^^^^^^^^^^^

.. java:constructor:: public UIController(String urlUiBackend)
   :outertype: UIController

Methods
-------
add
^^^

.. java:method:: @PostMapping public String add(ItemToAdd item, HttpSession session)
   :outertype: UIController

cart
^^^^

.. java:method:: @GetMapping public String cart(Model model, HttpSession session)
   :outertype: UIController

confirm
^^^^^^^

.. java:method:: @GetMapping public String confirm(Model model, HttpSession session)
   :outertype: UIController

confirm
^^^^^^^

.. java:method:: @PostMapping public String confirm(PaymentDetails details, Model model, HttpSession session)
   :outertype: UIController

delete
^^^^^^

.. java:method:: @PostMapping public RedirectView delete(ItemToAdd item, RedirectAttributes redirectAttributes, HttpSession session)
   :outertype: UIController

index
^^^^^

.. java:method:: @GetMapping public String index(Model model)
   :outertype: UIController

products
^^^^^^^^

.. java:method:: @GetMapping public String products(Model model)
   :outertype: UIController

