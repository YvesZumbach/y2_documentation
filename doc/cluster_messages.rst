.. _cluster-messages:

Cluster Messages
================

This pages describes all the messages exchange in the y2 cluster, more or less in the order they are to be sent.

Cluster Initialization
----------------------

``ClientRequest``
^^^^^^^^^^^^^^^^^

Nodes must be started before the client service.
Nodes will listen to all akka ``MemberUp`` message that are sent when a new actor is added to the cluster.
If this member has the ``client`` role, then the node will send a ``ClientRequest`` message.

``ClientAnswer``
^^^^^^^^^^^^^^^^

When the client receive a ``ClientRequest`` message, it saves the reference to the node and answers with a ``ClientRequest`` message.
The node, when receiving the ``ClientAnswer`` message, will save the reference to the client.

.. _node_index_message:

``NodeIndex``
^^^^^^^^^^^^^

The total number of node in the cluster must be given as argument to the client service when starting it.
Once all nodes have registered themselves to the client service, the client service will start the training process by sending to each node its id in the cluster (from ``0`` to ``nodeCount-1``) and the total number of node in the cluster ``nodeCount``. Nodes will begin the training as soon as they receive their id and the total node count.

Each ``NodeIndex`` messages is composed of:

1. The id of a node in the cluster.
2. The total number of nodes in the cluster

These information allow the worker to compute which data it must train on: samples from :math:`\lfloor \frac{\texttt{nodeId}}{\texttt{nodeCount}}\cdot\texttt{trainingSetSize}\rfloor` (inclusive) to  :math:`\lfloor\frac{\texttt{nodeId} + 1}{\texttt{nodeCount}}\cdot \texttt{trainingSetSize}\rfloor` (exclusive).
As soon as the worker receive this message it will start training.

Running the Cluster
-------------------

``Delta``
^^^^^^^^^

Deltas to apply to the weight of the NN are transmitted in a compressed form.
One delta is transmitted as a single 4 byte integer.
The 31 most significant bits encode the index of the weight to modify.
The least significant bit encode whether the delta is positive or negative.

The index encoding is further divided in three parts:

1. The index of the layer containing the weight to modify on the 9 most significant bits (thus limiting the maximum number of layers to 512).
2. Whether we are changing a weight or a bias (it is useful because PyTorch encodes weights and biases in two different arrays).
   1 means a weight, 0 means a bias.
3. The index of the weight/bias to modify in the given layer on the remaining 21 least significant bits (thus limiting the maximum number of weight to 2097152, which means that, in a densely connected layer, ou cannot have more than :math:`\lfloor\sqrt{2097152}\rfloor = 1448` neurons).

The value of the delta itself is a cluster variable and is known in advance, therefor it is not sent.
