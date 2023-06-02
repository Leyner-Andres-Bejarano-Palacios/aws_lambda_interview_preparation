# lambda_interview_preparation

## Theorical Questions Section

### Theorical Question 0

Apart of a zip file how else could you deploy a lambda ?

<details><summary><b>Answer</b></summary>

A container image that is compatible with the Open Container Initiative (OCI) specification.

</details>

<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/getting-started.html#lambda-settingup-author

https://www.youtube.com/watch?v=TGQVXnrIljg
</details>


### Theorical Question 1

Do you know what is the Lambda event source mappings ?

<details><summary><b>Answer</b></summary>

An event source mapping is a Lambda resource that reads from an event source and invokes a Lambda function. You can use event source mappings to process items from a stream or queue in services that don't invoke Lambda functions directly. 

</details>

<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/invocation-eventsourcemapping.html
</details>


### Theorical Question 2
How can you creat a batching behaviour for Lambda event source mappings ?

<details><summary><b>Answer</b></summary>

Event source mappings read items from a target event source. By default, an event source mapping batches records together into a single payload that Lambda sends to your function. To fine-tune batching behavior, you can configure a batching window (MaximumBatchingWindowInSeconds) and a batch size (BatchSize). A batching window is the maximum amount of time to gather records into a single payload. 

For Kinesis, DynamoDB, and Amazon SQS event sources: The default batching window is 0 seconds. This means that Lambda sends batches to your function as quickly as possible. If you configure a MaximumBatchingWindowInSeconds, the next batching window begins as soon as the previous function invocation completes.

For Amazon MSK, self-managed Apache Kafka, and Amazon MQ event sources: The default batching window is 500 ms. You can configure MaximumBatchingWindowInSeconds to any value from 0 seconds to 300 seconds in increments of seconds. A batching window begins as soon as the first record arrives.

Note
Because you can only change MaximumBatchingWindowInSeconds in increments of seconds, you cannot revert back to the 500 ms default batching window after you have changed it. To restore the default batching window, you must create a new event source mapping.

</details>

<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/invocation-eventsourcemapping.html
</details>

### Theorical Question 3
Do you know what a lambda layer is ?

<details><summary><b>Answer</b></summary>

A Lambda layer is a .zip file archive that can contain additional code or other content. A layer can contain libraries, a custom runtime, data, or configuration files.

Layers provide a convenient way to package libraries and other dependencies that you can use with your Lambda functions. Using layers reduces the size of uploaded deployment archives and makes it faster to deploy your code. Layers also promote code sharing and separation of responsibilities so that you can iterate faster on writing business logic.

You can include up to five layers per function.

</details>

<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-concepts.html#gettingstarted-concepts-layer
</details>

### Theorical Question 4
Do you know what a lambda destination is ?

<details><summary><b>Answer</b></summary>

A destination is an AWS resource where Lambda can send events from an asynchronous invocation. You can configure a destination for events that fail processing. Some services also support a destination for events that are successfully processed.
</details>

<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/gettingstarted-concepts.html#gettingstarted-concepts-destinations
</details>

### Theorical Question 5
Do you know what a lambda handler is ?

<details><summary><b>Answer</b></summary>

You tell Lambda the entry point to your function by defining a handler in the function configuration. The runtime passes in objects to the handler that contain the invocation event and the context, such as the function name and request ID.

When the handler finishes processing the first event, the runtime sends it another. The function's class stays in memory, so clients and variables that are declared outside of the handler method in initialization code can be reused. To save processing time on subsequent events, create reusable resources like AWS SDK clients during initialization. Once initialized, each instance of your function can process thousands of requests.

Your function also has access to local storage in the /tmp directory. The directory content remains when the execution environment is frozen, providing a transient cache that can be used for multiple invocations.
</details>

<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/foundation-progmodel.html
</details>

### Theorical Question 6
Do you know what a Lambda SnapStart is ?

<details><summary><b>Answer</b></summary>

When Lambda SnapStart is activated, the Init phase happens when you publish a function version. Lambda saves a snapshot of the memory and disk state of the initialized execution environment, persists the encrypted snapshot, and caches it for low-latency access. 
</details>

<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/foundation-progmodel.html
</details>

### Theorical Question 7
Do you undersstand what is reserved concurrency and provisioned concurrency?

<details><summary><b>Answer</b></summary>

To prevent a function from using too much concurrency, and to reserve a portion of your account's available concurrency for a function, use reserved concurrency. Reserved concurrency splits the pool of available concurrency into subsets. A function with reserved concurrency only uses concurrency from its dedicated pool.

To enable functions to scale without fluctuations in latency, use provisioned concurrency. For functions that take a long time to initialize, or that require extremely low latency for all invocations, provisioned concurrency enables you to pre-initialize instances of your function and keep them running at all times. Lambda integrates with Application Auto Scaling to support autoscaling for provisioned concurrency based on utilization.
</details>

<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/foundation-progmodel.html
</details>

### Theorical Question 8
Do you undersstand what happen when a runtime reaches end of support ?

<details><summary><b>Answer</b></summary>

Function invocations continue indefinitely after the runtime reaches end of support. However, AWS strongly recommends that you migrate functions to a supported runtime so that you continue to receive security patches and remain eligible for technical support

In almost all cases, the end-of-life date of a language version or operating system is known well in advance. The links below give end-of-life schedules for each language that Lambda supports as a managed runtime. In addition, Trusted Advisor includes a check that provides 120 days' notice of upcoming Lambda runtime end of support, and Lambda notifies you by email if you have functions using a runtime that is scheduled for end of support in the next 60 days.

</details>

<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/lambda-runtimes.html
</details>

### Theorical Question 9
How can you pre-load code during initialization in aws lambda ?

<details><summary><b>Answer</b></summary>

Lambda supports configuration-only ways to enable code to be pre-loaded during function initialization through the following language-specific environment variables:

JAVA_TOOL_OPTIONS – On Java, Lambda supports this environment variable to set additional command-line variables in Lambda. This environment variable allows you to specify the initialization of tools, specifically the launching of native or Java programming language agents using the agentlib or javaagent options. For more information, see JAVA_TOOL_OPTIONS environment variable.

NODE_OPTIONS – On Node.js 10x and above, Lambda supports this environment variable.

DOTNET_STARTUP_HOOKS – On .NET Core 3.1 and above, this environment variable specifies a path to an assembly (dll) that Lambda can use.

</details>

<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/runtimes-modify.html#runtimes-envvars
</details>

### Theorical Question 10
Do you know what the compute optimizer is ?

<details><summary><b>Answer</b></summary>

https://docs.aws.amazon.com/lambda/latest/dg/configuration-function-common.html#configuration-memory-optimization-accept

</details>

<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/configuration-function-common.html#configuration-memory-optimization-accept
</details>


### Theorical Question 11
How can you use lambda layers when you are dploying your lambdas using  ?

<details><summary><b>Answer</b></summary>

https://aws.amazon.com/blogs/compute/working-with-lambda-layers-and-extensions-in-container-images/

</details>

<details><summary><b>Source</b></summary>
https://aws.amazon.com/blogs/compute/working-with-lambda-layers-and-extensions-in-container-images/
</details>

### Theorical Question 12
why would you configure a stream responses ?

<details><summary><b>Answer</b></summary>

You can configure your Lambda function URLs to stream response payloads back to clients. Response streaming can benefit latency sensitive applications by improving time to first byte (TTFB) performance. This is because you can send partial responses back to the client as they become available. Additionally, you can use response streaming to build functions that return larger payload

</details>

<details><summary><b>Source</b></summary>
https://aws.amazon.com/blogs/compute/working-with-lambda-layers-and-extensions-in-container-images/
</details>

### Theorical Question 13
Do you understand what a dead-letter is ?

<details><summary><b>Answer</b></summary>

you can configure a standard Amazon SQS queue or standard Amazon SNS topic as a dead-letter queue for discarded events. For dead-letter queues, Lambda only sends the content of the event, without details about the response.

you can configure your function with a dead-letter queue to save discarded events for further processing. A dead-letter queue acts the same as an on-failure destination in that it is used when an event fails all processing attempts or expires without being processed. However, a dead-letter queue is part of a function's version-specific configuration, so it is locked in when you publish a version. On-failure destinations also support additional targets and include details about the function's response in the invocation record.

To reprocess events in a dead-letter queue, you can set it as an event source for your Lambda function. Alternatively, you can manually retrieve the events.

You can choose an Amazon SQS standard queue or Amazon SNS standard topic for your dead-letter queue.

</details>


<details><summary><b>Source</b></summary>
https://aws.amazon.com/blogs/compute/working-with-lambda-layers-and-extensions-in-container-images/
</details>

### Theorical Question 14
Do you know how many times does Event source mappings is re-executed in case of error?

<details><summary><b>Answer</b></summary>

Event source mappings that read from streams retry the entire batch of items. Repeated errors block processing of the affected shard until the error is resolved or the items expire. To detect stalled shards, you can monitor the Iterator Age metric.

For event source mappings that read from a queue, you determine the length of time between retries and destination for failed events by configuring the visibility timeout and redrive policy on the source queue. 

</details>


<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/invocation-retries.html
</details>


### Theorical Question 15
Do you understand why provisioned concurrency faster than reserved concurrency ?

<details><summary><b>Answer</b></summary>

You use reserved concurrency to define the maximum number of execution environments reserved for a Lambda function. However, none of these environments come pre-initialized. As a result, your function invocations may take longer because Lambda must first initialize the new environment before being able to use it to invoke your function. When Lambda has to initialize a new environment in order to carry out an invocation, this is known as a cold start. To mitigate cold starts, you can use provisioned concurrency.

</details>


<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/invocation-retries.html
</details>

### Theorical Question 16
What is the case when you shoulod use both reserved and provisioned concurrency ?

<details><summary><b>Answer</b></summary>

 In practice, you can set both provisioned concurrency and reserved concurrency on a function. You might do this if you had a function that handles a consistent load of invocations, but routinely sees spikes of traffic during the weekends.

</details>


<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/invocation-retries.html
</details>


### Theorical Question 17
HOw would you monitor lambda concurrency ?

<details><summary><b>Answer</b></summary>

https://docs.aws.amazon.com/lambda/latest/dg/monitoring-concurrency.html

</details>


<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/monitoring-concurrency.html
</details>


### Theorical Question 18
HOw would you monitor lambda concurrency ?

<details><summary><b>Answer</b></summary>

https://docs.aws.amazon.com/lambda/latest/dg/monitoring-concurrency.html

</details>


<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/monitoring-concurrency.html
</details>


### Theorical Question 19
establish a private connection between your VPC and Lambda ?

<details><summary><b>Answer</b></summary>

establish a private connection between your VPC and Lambda, create an interface VPC endpoint. Interface endpoints are powered by AWS PrivateLink.

Lambda purges idle connections over time, so you must use a keep-alive directive to maintain persistent connections. Attempting to reuse an idle connection when invoking a function results in a connection error. To maintain your persistent connection, use the keep-alive directive associated with your runtime

</details>


<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/configuration-vpc-endpoints.html
</details>

### Theorical Question 20
Lambda best practices

<details><summary><b>Answer</b></summary>

https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html

</details>


<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html
</details>

### Theorical Question 21
Do you know what is a AWS Lambda application

<details><summary><b>Answer</b></summary>

An AWS Lambda application is a combination of Lambda functions, event sources, and other resources that work together to perform tasks. You can use AWS CloudFormation and other tools to collect your application's components into a single package that can be deployed and managed as one resource. Applications make your Lambda projects portable and enable you to integrate with additional developer tools, such as AWS CodePipeline, AWS CodeBuild, and the AWS Serverless Application Model command line interface (AWS SAM CLI).

</details>


<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/lambda/latest/dg/best-practices.html
</details>

### Theorical Question 22
Do you undrstand what serverless mean

<details><summary><b>Answer</b></summary>

With AWS serverless technologies, you can build and run applications without having to manage your own servers. All server management is done by AWS, providing many benefits such as automatic scaling and built-in high availability, letting you take your idea to production quickly. Using serverless technologies, you can focus on the core of your product without having to worry about managing and operating servers.

</details>


<details><summary><b>Source</b></summary>
https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/what-is-concepts.html
</details>

