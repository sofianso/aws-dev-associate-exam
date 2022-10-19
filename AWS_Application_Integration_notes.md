# AWS Application Integration Notes

## AWS SQS

SQS stores queues messages in Queue, which is highly scalable by default. It allows the requests of data from one instance to another without being overloaded for in case there's a spike. In addition, it helps saves costs since the instance that is receiving the messages do not need to scale up, and instead, polls SQS to pull the messages.
It also guarantees that messages will be processed at least once.

### Standard Queue

- With Standard Queue, the consumer is not guaranteed that it will process the oldest message first.
- At-Least-Once-Delivery: The order in which messages are sent and received is strictly preserved.

### FIFO Queue

- With FIFO Queue, the consumer is guaranteed that it will process the oldest message first.
- Exactly-Once Processing: A message is delivered once and remains available until a consumer processes and deletes it. Duplicates are not introduced to the queue.

### Dead-Letter Queue

Dead-Letter Queue is used to handle message failure by setting aside messages that can't be processed correctly to determine why their processing didn't succeed. A couple of things to note:

- Do not implement this with FIFO queues because it will break the order of messages.
- It shouldn't be used with standard queues if the application will keep trying for transmission.

### Delay Queue

Delay Queue postpones new messages to a queue for a number of seconds. Thus, messages being sent to Delay Queue remain invisible to consumers for the duration of the delay period.

### Visibility Timeout

Visibility Timeout is the amount of time a message is invisible in the queue after a reader picks it up.

### Short Polling vs. Long Polling

Short polling will try to make multiple API calls even if the message is empty until it consumes a message from the queue.This means that it will increase costs since you are charged based on the number API calls made.

Long polling means that the consumer will wait before it tries to consume the message. This method allows less API calls which should result in reducing costs.

If `ReceiveMessageWaitTimeSeconds` / `WaitTimeSeconds` is greater than 0, then it is long polling but if it stays at 0 then it is short polling.

## Amazon SQS - API

- ChangeMessageVisibility changes the visibility of a specified message in a queue to a new value.
- GetAttributes and SetQueueAttributes gets/sets attributes for the specified queue.
- DelaySeconds configures a delay queue.
- VisibilityTimeout is the amount of time a message is invisible in the queue after a reader picks it up.
- ReceiveMessage
  - WaitTimeSeconds enables long-poll support
- SendMessage
  - DelaySeconds parameter delays a message
  - MessageDeduplicationId parameter adds a deduplication (FIFO only)
  - MessageGroupId parameter adds a tag for message group (FIFO only)

## AWS SNS
