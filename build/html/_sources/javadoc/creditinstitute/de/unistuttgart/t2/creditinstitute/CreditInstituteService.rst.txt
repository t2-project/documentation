.. java:import:: java.util Random

.. java:import:: de.unistuttgart.t2.creditinstitute.domain PaymentData

.. java:import:: de.unistuttgart.t2.creditinstitute.exceptions PaymentFailedException

CreditInstituteService
======================

.. java:package:: de.unistuttgart.t2.creditinstitute
   :noindex:

.. java:type:: public class CreditInstituteService

   Fakes the payment.

   Probabilities for failure and timeouts, disregarding all network delay, are as follows:

   assuming the payment calls the provide with a timeout of t_max, then the probability of a timeout is:

   p(timeout) = ((1 - failurerate) * timeoutrate) + p(random timeout)

   with: p(random timeout) = (1 - failurerate) * (1 - timeoutrate) * p (X > * t_max)

   with: p(X > t_max) = ((timeout/2 - t_max) / timeout) iff timeout/2 >= t_max or: p(X > t_max) = 0 otherwise

   the probability of a functional failure (HTTP response with status code 500 Internal Server Error) is equal to failurate.

   Both rates and the timeout duration can be adjusted via the respective http endpoints.

   :author: maumau

Methods
-------
doPayment
^^^^^^^^^

.. java:method:: public void doPayment(PaymentData data) throws Exception
   :outertype: CreditInstituteService

   Fake executes some payment. Depending on \ :java:ref:`failurerate <CreditInstituteService.failurerate>`\ , \ :java:ref:`timeoutrate <CreditInstituteService.timeoutrate>`\  and \ :java:ref:`timeout <CreditInstituteService.timeout>`\  this operation either throws an exception or delays up to \ :java:ref:`timeoutrate <CreditInstituteService.timeoutrate>`\  milliseconds.

   :param data: informations usually found on a credit card
   :throws Exception: if anything 'failed'

getFailurerate
^^^^^^^^^^^^^^

.. java:method:: public double getFailurerate()
   :outertype: CreditInstituteService

getTimeout
^^^^^^^^^^

.. java:method:: public int getTimeout()
   :outertype: CreditInstituteService

getTimeoutrate
^^^^^^^^^^^^^^

.. java:method:: public double getTimeoutrate()
   :outertype: CreditInstituteService

setFailurerate
^^^^^^^^^^^^^^

.. java:method:: public void setFailurerate(double failurerate)
   :outertype: CreditInstituteService

   Update the failure rate.

   The new value must not be negative. If it is, the current value remains unchanged.

   :param failurerate: probability for failures as decimal

setTimeout
^^^^^^^^^^

.. java:method:: public void setTimeout(int timeout)
   :outertype: CreditInstituteService

   Update the timeout duration.

   The new value must not be negative. If it is, the current value remains unchanged.

   :param timeout: duration of timeout in ms

setTimeoutrate
^^^^^^^^^^^^^^

.. java:method:: public void setTimeoutrate(double timeoutrate)
   :outertype: CreditInstituteService

   Update the timeout rate.

   The new value must not be negative. If it is, the current value remains unchanged.

   :param timeoutrate: probability for timeouts as decimal

