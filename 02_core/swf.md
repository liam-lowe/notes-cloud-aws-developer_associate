# SWF - Simple Workflow Service

## Summary

Coordinates work amongst applications.

Code runs on EC2 (not serverless)

1 year max runtime

Concept of an *activity step* and *decision step*.

Has a built in *Human Intervention Step*.

Step functions is recommended to be used for new applications, except:

- If you need external signals to intervene in the processes
- If you need child processes that return values to parent processes.

## Security

## Use Case

Order fulfillment from web to warehouse to delivery.

## Cost
