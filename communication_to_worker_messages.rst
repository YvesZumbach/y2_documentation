
Communication to Worker Messages
================================

When the communication service and the worker service exchange messages, they always follow the following protocol:

1. Send 4 bytes in big endian order containing the size of the message to come
2. Send the actual message whose size must match the previously sent size.