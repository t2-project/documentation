.. _microservices:

========================
T2-Project Microservices
========================

The T2-Project consists of seven services that realize the store's business logic plus two additional services, one to simulate an external payment provider, as an example credit institute, and the other to test the store at runtime (e2e).

All services are Spring Boot applications. 
They are instrumented with `Prometheus <https://prometheus.io/>`__ for metrics and with `Jaeger <https://www.jaegertracing.io/>`__  for tracing.

See page :doc:`Architecture <arch>` for more information about the microservices architecture.
See pages :doc:`Usage <use>` and :doc:`Deployment <deploy>` for more information about how to use the T2-Project.
