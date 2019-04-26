
Running A y2 Cluster
====================

Prerequisites
-------------

To run a y2 cluster, you must know in advance:

1. How many node will be part of the cluster
2. The IP of one of these nodes.

The first requirement allow the client to know when all the nodes have registered in order to launch the cluster only when all nodes are ready.
Node need to be part of the cluster from the start in order to keep an up-to-date version of the trained NN; so dynamicly joining is really an option here.
If a node was to join the cluster late, it would not receive the first Delta messages containing the update to apply to the NN and could prevent the proper convergence of the NN.

Starting the Nodes
------------------

Starting a node is done by executing:

``y2 node --seed-ip <IP>``.

Start by launching the node whose IP you will use as seed IP.
Start all the remaining nodes.

Starting the Client
-------------------

Once all the nodes are started, start the client: 

``y2 client --node-count <nodeCount> --seed-ip <IP>``.

That's it!
The cluster is started and training probably has already begun as we speak.
