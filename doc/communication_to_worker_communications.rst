.. _communication-to-worker:

Communication Service to Worker Service Communications
======================================================

Data Representation
-------------------

* Integers are always sent as 4 bytes signed values in big endian order.

Communication Protocol
----------------------

The convention is identical in both communication directions.
When the communication service and the worker service exchange messages, they always follow the following protocol:

1. Send an 8 bytes message, called handshake, containing, in big endian order, first the type of message as an integer, then the size of the message to come as an integer.
2. Send the actual message whose size must match the previously sent size.

.. note::
   Some message (like the :ref:`node_index_message` messages) have a fixed size.
   Nevertheless, the size sent in the first message must always be correct.

Message Types
-------------

Messages sent between the communication service and the worker service are enumerated hereafter.
The integer value is the message type value.

* ``NodeIndex``: ``0``
* ``Delta``: ``1``
