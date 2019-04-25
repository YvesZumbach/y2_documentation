
Cluster Messages
================

Deltas to apply to the weight of the NN are transmitted in a compressed form.
One delta is transmitted as a single 4 byte integer.
The 31 most significant bits encode the index of the weight to modify.
The least significant bit encode whether the delta is positive or negative.

The value of the delta itself is a cluster variable and is known in advance, therefor it is not sent.