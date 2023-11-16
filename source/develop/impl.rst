====================
Implementation Notes
====================

Here we list a few notes about the technical implementation.

* The *T2-Modulith* application and the *UI* service get packaged as a ``war`` and not as ``jar``, because of the limitations of JSP used for the UI (see Spring Docs about `JSP Limitations <https://docs.spring.io/spring-boot/docs/current/reference/html/web.html#web.servlet.embedded-container.jsp-limitations>`_\ )
* Default port of the *T2-Modulith* is set to 8081 to have the same base URL than the `T2-Project UI Backend Service <https://github.com/t2-project/uibackend>`_
* You can change many application properties in the ``application-*.yaml`` files under :file:`./src/main/resources/`. The properties are documented in the README of the individual application/service (see e.g. `modulith repository <https://github.com/t2-project/modulith#application-properties>`_.
