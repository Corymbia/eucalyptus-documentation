+++
title = "Simple Queue Service Concepts"
weight = 10
+++

This section describes the important concepts for the Simple Queue Service (SQS)

### Queues and Queue URLs

A queue is a named destination for messages in an account. A queue has a URL that uniquely identifies it on the cloud.

### Delivery and Visiblity

When a message is delivered to a client it is hidden from other clients for a period to prevent duplicate handling. If the message is not handled by the first client it will later become visible for handling by other clients.

### Dead-letter Queues

A dead-letter queue can be used for undeliverable messages. Using a dead-letter queue allows for handling of messages that would otherwise not be processed.

### Delay Queue

A delay queue allows messages to be available from a queue after a delay period rather than as soon as messages are sent to the queue.

### Polling Style

Short or long polling can be used when receiving messages. For short polling there is an immediate response whether a message is available or not. For long polling a delay of up to 20 seconds is used and the response will occur when a message is available or when the given timeout is reached even if there is no message.
