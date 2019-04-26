
Cluster Architecture
====================

The y2 cluster is based on a master-slave architecture.
The master is called **client**, while the slaves are called **nodes**.

The client manages the whole cluster and serves as a centralized end-point.
It is used to issue commands that require knowledge of the whole system (like which data should a given node train on) and it act as a sink for logging messages.

.. figure:: cluster_architecture_graphs/cluster_architecture.png
    :width: 80%

    Architecture of the y2 cluster.

Each node is itself composed of two services:

1. A communication service
2. A worker service

.. figure:: cluster_architecture_graphs/node_architecture.png
    :width: 80%

    Architecture of a single node of the y2 cluster.

The communication service handles the connection with the rest of the y2 cluster.
The worker service is the one that actually performs the training.
Such a decomposition was chosen because it allowed using very targeted technologies for each of these specific tasks (Scala and akka for the cluster part, PyTorch for the training part)
