# Step Functions

- Step Functions allow users to model workflows as state machines
- In essence, Step Functions are sequences of AWS service calls
- *Workflows* are JSON defined sets of instructions
- Workflows can be started using SDK calls, API Gateway, or Event Bridge
- *Tasks* are steps in a workflow
- *Task States* are used to do work in a state machine
- Step Funtions supports a graphical builder to create workflows

## States Types

- *Choice States* test for a condition to send to a branch
- *Fail/Succeed States* stop execution
- *Pass States* pass input to output or inject fixed data
- *Wait States* waits for a specified amount of time or until a condition is met
- *Map States* dynamically iterate steps
- *Parallel States* begin parallel branches of execution
