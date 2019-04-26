.. _communication-to-worker-messages:

Communication Service to Worker Service Messages
================================================

Data Representation
-------------------

* Integers are always sent as 4 bytes signed values in big endian order.

Communication Protocol
----------------------

When the communication service and the worker service exchange messages, they always follow the following protocol:

1. Send 4 bytes in big endian order containing the size of the message to come.
2. Send the actual message whose size must match the previously sent size.

Convention
----------

The first message sent by the communication service to the worker service is a message that contains two integers:

1. The id of the node in the cluster.
2. The total number of nodes in the cluster

These information allow the worker to compute which data it must train on: samples from :math:`\lfloor \frac{\texttt{nodeId}}{\texttt{nodeCount}}\cdot\texttt{trainingSetSize}\rfloor` (inclusive) to  :math:`\lfloor\frac{\texttt{nodeId} + 1}{\texttt{nodeCount}}\cdot \texttt{trainingSetSize}\rfloor` (exclusive).
As soon as the worker receive this message it will start training.

All subsequent messages will only contain deltas to apply.
