# Batch Flow

## Batch Process AWS ECS Task Submission
This is the sequence diagram for the Batch Process task submission. 

When we receive a request containing multiple LinkedIn profiles, we defer the processing of this request by submitting an [ECS RunTask Request](https://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/com/amazonaws/services/ecs/model/RunTaskRequest.html).

![Batch Flow](/images/batch-flow.png "Batch Flow: Sequence Diagram")

## Batch Processor (ECS Task)
This is the sequence diagram for the Batch Processor ran as a task in an [ECS](https://aws.amazon.com/ecs/) Container.

![Batch Processor](/images/batch-processor.png "Batch Processor: Sequence Diagram")