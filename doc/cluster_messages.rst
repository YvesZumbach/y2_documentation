.. _cluster-messages:

Cluster Messages
================

This pages describes all the messages exchange in the y2 cluster, more or less
in the order they are to be sent.

Cluster Initialization
----------------------

``ClientRequest``
^^^^^^^^^^^^^^^^^

Nodes must be started before the client service.
Nodes will listen to all akka ``MemberUp`` message that are sent when a new
actor is added to the cluster. If this member has the ``client`` role, then
the node will send a ``ClientRequest`` message.

``ClientAnswer``
^^^^^^^^^^^^^^^^

When the client receive a ``ClientRequest`` message, it saves the reference
to the node and answers with a ``ClientRequest`` message. The node, when
receiving the ``ClientAnswer`` message, will save the reference to the client.

``NodeIndex``
^^^^^^^^^^^^^

The total number of node in the cluster must be given as argument to the client
service when starting it. Once all nodes have registered themselves to the
client service, the client service will start the training process by sending
to each node its id in the cluster (from ``0`` to ``nodeCount-1``) and the
total number of node in the cluster ``nodeCount``. Node will begin the training
as soon as they receive their id and the total node count.

Running the Cluster
-------------------

``Delta``
^^^^^^^^^

Deltas to apply to the weight of the NN are transmitted in a compressed form.
One delta is transmitted as a single 4 byte integer.
The 31 most significant bits encode the index of the weight to modify.
The least significant bit encode whether the delta is positive or negative.

The value of the delta itself is a cluster variable and is known in advance,
therefor it is not sent.
