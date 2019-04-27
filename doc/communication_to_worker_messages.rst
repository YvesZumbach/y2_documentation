.. _communication-to-worker-messages:

Communication Service to Worker Service Messages
================================================

Data Representation
-------------------

* Integers are always sent as 4 bytes signed values in big endian order.

Communication Protocol
----------------------

The convention is identical in both communication directions.
When the communication service and the worker service exchange messages, they always follow the following protocol:

1. Send an 8 bytes message, called handshake, containing, in big endian order, first the type of message as an integer, then the size of the message to come as an integer.
2. Send the actual message whose size must match the previously sent size.

.. note:: Size must always be correct
   Some message (like the :ref:`node_index_message` messages) have a fixed size.
   Nevertheless, the size sent in the first message must always be correct.

Message Types
-------------

Messages sent between the communication service and the worker service are enumerated hereafter.
The integer value is the message type value.

* ``NodeIndex``: ``0``
* ``Delta``: ``1``

``NodeIndex``
-------------

The first message generally sent by the communication service to the worker service is a ``NodeIndex`` message that contains two integers:

1. The id of the node in the cluster.
2. The total number of nodes in the cluster

These information allow the worker to compute which data it must train on: samples from :math:`\lfloor \frac{\texttt{nodeId}}{\texttt{nodeCount}}\cdot\texttt{trainingSetSize}\rfloor` (inclusive) to  :math:`\lfloor\frac{\texttt{nodeId} + 1}{\texttt{nodeCount}}\cdot \texttt{trainingSetSize}\rfloor` (exclusive).
As soon as the worker receive this message it will start training.

``Delta``
---------

TODO