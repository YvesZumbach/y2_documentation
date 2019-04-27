
y2 Command
==========

The whole y2 cluster is manged from a single command ``y2``.
This command takes a first mandatory argument: the program to execute (``client`` or ``node``).

The options are documented hereafter::

   y2 v1.0 The base command to handle a y2 cluster.
   Usage: y2 [client|node]

   Command: client [options]
   An y2 cluster entry point, also known as 'a client'.
   -n, --node-count <value>
                              The number of nodes that will be part of the cluster (needed to compute which node will train on which data).
   -s, --seed-ip <value>    The IP address to use to enter the cluster (must an external IP). If you are starting the first node of th cluster, use the external IP of the node.

   Command: node [options]
   An y2 cluster work-horse, also known as 'a node'.
   -l, --local <value>      If true, a local cluster of three nodes will be started, otherwise, start just on node.
   --local-node-count <value>
                              The number of local node to run.
   -s, --seed-ip <value>    The IP address to use to enter the cluster (must an external IP). If you are starting the first node of th cluster, use the external IP of the node.

This helper message will be printed if you type ``y2``.