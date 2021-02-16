# SQS - Simple Queue Service

## Summary

Simple Queue Service (SQS) is a service that manages and operates message oriented middleware. It enables you to decouple and scale microservices, distributed systems, and serverless apllications.

### Summary - What's a queue?

A form of asynchronous service-to-service communication used in multiple application architectures.

Messages are stored on the queue until they are processed and deleted.

### Summary - Standard Queue

- Oldest offering from AWS (over 10 years old)
- Fully managed service
- Scales from 1 message per second to 10,000 messages per second
- Default retention: 4 days
- Max retention: 14 days
- There is no limit to how many messages can be in the queue
- Low latency (10ms publish / receive)
- Horizontal scaling in number of consumers
- Can have duplicate messages
- Can have messages out of order (best effort ordering)
- Limitation of 256kb per message

### Summary - Delay

- Delays a message so a consumer doesn't see it immediatel
  - Up to 15 minute delay
- Default is 0 seconds, making messages available straight away
- You can set the default delay at the queue level
- You can override the default using the `DelaySeconds` parameter

### Summary - Producing Messages

- Define the body
- Add message attributes (metadata - optional)
- Optionally can provide `DelaySeconds`
- You receive back:
  - Message identifier
  - MD5 hash of the body

### Summary - Consuming Messages

- Poll SQS for messages
  - Receive up to 10 at a time
- Next step is to process the message within the visibility timeout
- Finally, delete the message using the `MessageID` & Receipt Handle

### Summary - Visibility Timeout

- When a consumer polls a message from a queue, the message is *invisible* to other consumers for a defined period called `VisibilityTimeout`
  - Can be set between 0 seconds and 12 hours
  - Default 30 seconds
  - Example:
    - If it takes 15 minutes or longer to process, and fails, you must wait before processing again
    - If set to 30 seconds or lower and the consumer needs time to process the message, another consumer will receive the message it will be processed more than once
  - `ChangeMessageVisbility`
    - An API to change the visibility *while* processing the message
  - `DeleteMessage`
    - An API to tell SQS the message was successfully processed

### Summary - Dead Letter Queue

- If a consumer fails to consumer a message within the visibility timeout, the message goes back to the queue. We can put a threshold for how many times a message can be put back into the queue.
- After `MaximumReceives` times the threshold is is exceeded, the message goes into a Dead Letter Queue (DLQ)
  - DLQ is useful for debugging
  - Retention times for the messages should be set to max (14 days) for a DLQ
  - DLQ is a queue which is created separately, and attached to the normal queue

### Summary - Long Polling

- When a consumer requests for a message from a queue, it can optionally wait for messages to arrive in case there is no available messages to be consumer in the queue
- Long polling decreases the number of API calls made to SQS while increasing the efficiency and latency of the application.
- The wait time can be set to 1 second, up to 20 seconds
- Long polling should be preferred in case of short polling (wait time of 0 seconds)
- Long polling is enabled by setting a value between 1 and 20 seconds for `WaitTimeSeconds` queue attribute

### Summary - SQS Extended Client

- Message size limit is 256KB, Extended Client Library offers an implementation for larger messages using S3
- The data is uploaded to S3, the message will contain a pointer to the data. When the messafe the message is consumer, the data is retrieved from the S3 bucket using the pointer

### Summary - SQS API

- `CreateQueue(MessageRetentionPeriod)`: creates a queue
- `DeleteQueue`: deletes a queue
- `PurgeQueue`: deletes all the messages from a queue
- `SendMessage(DelaySeconds)`: send a message with optional delay
- `ReceiveMessageWaitTimeSeconds`: receives a message using long polling
- `ChangeMessageVisibility`: changes the message wait time in case there's more time needed for processing

Batch APIs are available for `SendMessage`, `DeleteMessage`, `ChangeMessageVisibility`

### Summary - FIFO Queues

- FIFO = First In, First Out
- Provides ordering of messages in a queue
- Has limited throughput compared to standard queues:
  - 300 messages per second
  - 3000 messages per second with batching
- Exactly-once send capability
- Messages are processed in order by the consumer
- Queues which are created as FIFO should have their name ending with "fifo"

#### Summary - FIFO Queues - Deduplication

- Used for making sure a message is sent only once
- Deduplication interval is 5 minutes
- Deduplication methods:
  - Content based deduplication: the message body is hashed with SHA-256 algorithm and the hash is used to detect duplicates
  - `MessageDeduplicationID`: attribute can be set explicityly for checking duplicates

#### Summary - FIFO Queues - Message Grouping

- `MessageGroupID`: if this attribute is set, a message group can only have one consumer, and the messages will arrive in order for the same message group
- Provides ordering at a subset level of messages in case of a queue:
  - Messages which share the same group id arrive in order within the group
  - Each group id can have a different consumer
  - A queue can have multiple groups
  - Ordering accross the groups is not guaranteed

## Security

## Use Case

## Cost
