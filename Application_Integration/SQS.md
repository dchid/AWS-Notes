# SQS

---

- *Amazon Simple Queue Service (SQS)* is a hosted queue used to integrate and decouple software systems and components

## Features

- There are no limits to the number of messages that can be stored in an SQS Queue

### Dead Letter Queue

- If a message repeatedly gets returned to the queue, it gets sent to a *Dead Letter Queue (DLQ)*
- Messages get sent to a DQL after exceeding the `MaximumReceives` threshold
- The message retention period defines how long messages stay in the DLQ before deletion
- Ensure to process messages in DLQ before they're deleted
- *Redrive to Source* is a feature to debug messages in DLQ and return them to the source queue
- Redrive policies are JSON objects
