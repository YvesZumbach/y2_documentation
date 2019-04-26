
y2 Command
==========

The whole y2 cluster is manged from a single command ``y2``.
This command takes a first mandatory argument: the program to execute (``client`` or ``node``).

The options are documented hereafter::

   y2 v1.0
   Usage: y2 [client|node]
   The base command to handle a y2 cluster.

   Command: client [options]
   An y2 cluster entry point, also known as 'a client'.
   -n, --node-count <value>   The number of nodes that will be part of the cluster (needed to compute which node will train on which data).

   Command: node [options]
   An y2 cluster work-horse, also known as 'a node'.
   -l, --local <value>        if true, a local cluster of three nodes will be started, otherwise, start just on node.
   --local-node-count <value> the number of local node to run.

This helper message will be printed if you type ``y2``.