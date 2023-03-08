---
title: AWS Lambda: Building Serverless Functions for Event-Driven Applications
description: 
published: true
date: 2023-02-19T00:33:33.571Z
tags: 
editor: markdown
dateCreated: 2023-02-19T00:33:32.053Z
---

- [AWS Lambda: 이벤트 기반 애플리케이션을 위한 서버리스 기능 구축***Korean** document is available*](/ko/Knowledge-base/Cloud/aws-lambda-building-serverless-functions-for-event-driven-applications)
{.links-list}



# AWS Lambda: Building Serverless Functions for Event-Driven Applications

AWS Lambda is a serverless compute service that runs your code in response to events and automatically manages the underlying compute resources for you. You can use AWS Lambda to build applications that respond quickly to new information. For example, an event-driven application can process log files as they are delivered by Amazon Simple Storage Service (Amazon S3) or Amazon Kinesis and perform actions such as storing log data in Amazon DynamoDB, sending alerts through Amazon Simple Notification Service (Amazon SNS), or invoking AWS Lambda functions to perform additional processing.

With Lambda, you can run code for virtually any type of application or backend service - all with zero administration. Just upload your code and Lambda takes care of everything required to run and scale your code with high availability. You can set up your code to automatically trigger from other AWS services or call it directly from any web or mobile app.

Lambda runs your code on a high-availability compute infrastructure and performs all of the administration of the compute resources, including server and operating system maintenance, capacity provisioning, and code monitoring and logging. All you need to do is supply the code.

## Getting Started with AWS Lambda

To get started with AWS Lambda, create a Lambda function and then configure an event source for the function. An event source is an AWS service or developer-created application that produces events that trigger an AWS Lambda function to run. For example, a Lambda function can be triggered when an object is created in an Amazon S3 bucket, when a message is published to an Amazon Simple Notification Service (Amazon SNS) topic, or when an Amazon DynamoDB table is updated.

When you create a Lambda function, you specify the events that trigger the function and the code that processes the event. When one of the specified events occurs, Lambda runs your code. Lambda provides a set of predefined event sources, and you can also add your own event sources.

To create a Lambda function:

1. Open the Lambda console.

2. In the navigation panel, choose Functions.

3. Choose Create function.

4. Select Author from scratch.

5. In the Function name field, enter a name for your function.

6. In the Runtime drop-down, select the language for your function.

7. For Role, select Choose an existing role.

8. In the Existing role drop-down, select a role that gives Lambda permissions to access resources in your account, such as Amazon S3 or Amazon DynamoDB. For more information, see Creating a Role for Lambda Functions.

9. Choose Create function.

Your function is created and displayed in the Functions list.

## Configuring an Event Source

After you create a Lambda function, you need to configure an event source for the function. When you configure an event source, you specify the event source type and the parameters required by that event source type. For example, if you are using an Amazon Kinesis stream as your event source, you need to specify the Amazon Kinesis stream name and Arn.

Lambda processes events from your event sources sequentially. To process events in parallel, create multiple, identical Lambda functions and configure each function with a different event source. For more information, see Using AWS Lambda with Amazon Kinesis.

You can configure an event source when you create a function, or you can add an event source later.

To configure an event source when you create a function:

1. Open the Lambda console.

2. In the navigation panel, choose Functions.

3. Choose Create function.

4. Select Author from scratch.

5. In the Function name field, enter a name for your function.

6. In the Runtime drop-down, select the language for your function.

7. Choose Create function.

8. In the Function code editor, enter your code.

9. In the designer, choose Add trigger.

10. In the Trigger configuration section, choose an event source type.

11. For Event source, choose an event source.

12. Configure the event source.

13. Choose Add.

Your function is created and displayed in the Functions list.

To add an event source later:

1. Open the Lambda console.

2. In the navigation panel, choose Functions.

3. Choose the name of the function that you want to add an event source to.

4. In the Function code editor, enter your code.

5. In the designer, choose Add trigger.

6. In the Trigger configuration section, choose an event source type.

7. For Event source, choose an event source.

8. Configure the event source.

9. Choose Add.

## Lambda Function Code

Lambda functions are written in the language of your choice. Lambda provides a set of predefined environments for each language that include the AWS SDK. With the AWS SDK, you can call AWS services from your Lambda function code. For example, you can use Amazon S3 to store data, Amazon DynamoDB to read and write data, or Amazon Simple Queue Service (Amazon SQS) to send and receive messages.

Lambda also provides a runtime API, which you can use to call services that are not available in the AWS SDK, or to call AWS SDK operations that are not available in the Lambda console. For more information, see AWS Lambda Runtime API.

## Lambda Function Handler

The handler is the entry point to your Lambda function. When Lambda executes your function, it passes the event data as a parameter to the handler. In return, the handler must return the data back to Lambda. The structure of the event data depends on the event source. For example, the event data from Amazon S3 contains information about the object that triggered the event, such as the file name and size. The event data from Amazon DynamoDB contains information about the item that was updated or deleted.

The handler must be a method in your code that uses the following format:

```{language}
def handler_name(event, context):
```

where handler_name is the name of the method, event is the parameter that contains the event data, and context is the parameter that contains information about the invocation, function, and execution environment.

For more information about the handler, see Lambda Function Handler in Python.

## Lambda Function Configuration

When you create or update a Lambda function, you specify function configuration information, such as the function name, description, entry point, runtime, and IAM role. You also specify the function code and any dependencies that your code requires, such as AWS SDK libraries.

## Lambda Function IAM Role

When you create a Lambda function, you specify an IAM role that Lambda uses to work with AWS resources on your behalf. For example, if your Lambda function reads and writes data to Amazon S3 buckets or Amazon DynamoDB tables, you need to grant the function permission to access those resources. You do this by creating an IAM role and attaching policies that identify the resources that the function can access. For more information, see Creating a Role for Lambda Functions.

## Lambda Function Policy

In addition to the IAM role that you specify when you create a Lambda function, Lambda also attaches a policy to the function's IAM role. The policy grants the function permission to log events to Amazon CloudWatch Logs and to write trace data to X-Ray. For more information, see Logging Lambda Function Activity to CloudWatch Logs.

## Lambda Function Execution Role

When you create a Lambda function, you specify an execution role. The execution role grants Lambda permissions to access AWS resources that your function needs to perform its tasks. For example, if your Lambda function reads and writes data to Amazon S3 buckets or Amazon DynamoDB tables, you need to grant the function permission to access those resources. You do this by creating an IAM role and attaching policies that identify the resources that the function can access. For more information, see Creating a Role for Lambda Functions.

## Lambda Function Handler and Role

The handler is the entry point to your Lambda function. When Lambda executes your function, it passes the event data as a parameter to the handler. In return, the handler must return the data back to Lambda. The structure of the event data depends on the event source. For example, the event data from Amazon S3 contains information about the object that triggered the event, such as the file name and size. The event data from Amazon DynamoDB contains information about the item that was updated or deleted.

The handler must be a method in your code that uses the following format:

```{language}
def handler_name(event, context):
```

where handler_name is the name of the method, event is the parameter that contains the event data, and context is the parameter that contains information about the invocation, function, and execution environment.

For more information about the handler, see Lambda Function Handler in Python.

## Lambda Function Configuration

When you create or update a Lambda function, you specify function configuration information, such as the function name, description, entry point, runtime, and IAM role. You also specify the function code and any dependencies that your code requires, such as AWS SDK libraries.

## Lambda Function IAM Role

When you create a Lambda function, you specify an IAM role that Lambda uses to work with AWS resources on your behalf. For example, if your Lambda function reads and writes data to Amazon S3 buckets or Amazon DynamoDB tables, you need to grant the function permission to access those resources. You do this by creating an IAM role and attaching policies that identify the resources that the function can access. For more information, see Creating a Role for Lambda Functions.

## Lambda Function Policy

In addition to the IAM role that you specify when you create a Lambda function, Lambda also attaches a policy to the function's IAM role. The policy grants the function permission to log events to Amazon CloudWatch Logs and to write trace data to X-Ray. For more information, see Logging Lambda Function Activity to CloudWatch Logs.

## Lambda Function Execution Role

When you create a Lambda function, you specify an execution role. The execution role grants Lambda permissions to access AWS resources that your function needs to perform its tasks. For example, if your Lambda function reads and writes data to Amazon S3 buckets or Amazon DynamoDB tables, you need to grant the function permission to access those resources. You do this by creating an IAM role and attaching policies that identify the resources that the function can access. For more information, see Creating a Role for Lambda Functions.

## Lambda Function Handler and Role

The handler is the entry point to your Lambda function. When Lambda executes your function, it passes the event data as a parameter to the handler. In return, the handler must return the data back to Lambda. The structure of the event data depends on the event source. For example, the event data from Amazon S3 contains information about the object that triggered the event, such as the file name and size. The event data from Amazon DynamoDB contains information about the item that was updated or deleted.

The handler must be a method in your code that uses the following format:

```{language}
def handler_name(event, context):
```

where handler_name is the name of the method, event is the parameter that contains the event data, and context is the parameter that contains information about the invocation, function, and execution environment.

For more information about the handler, see Lambda Function Handler in Python.

## Lambda Function Configuration

When you create or update a Lambda function, you specify function configuration information, such as the function name, description, entry point, runtime, and IAM role. You also specify the function code and any dependencies that your code requires, such as AWS SDK libraries.

## Lambda Function IAM Role

When you create a Lambda function, you specify an IAM role that Lambda uses to work with AWS resources on your behalf. For example, if your Lambda function reads and writes data to Amazon S3 buckets or Amazon DynamoDB tables, you need to grant the function permission to access those resources. You do this by creating an IAM role and attaching policies that identify the resources that the function can access. For more information, see Creating a Role for Lambda Functions.

## Lambda Function Policy

In addition to the IAM role that you specify when you create a Lambda function, Lambda also attaches a policy to the function's IAM role. The policy grants the function permission to log events to Amazon CloudWatch Logs and to write trace data to X-Ray. For more information, see Logging Lambda Function Activity to CloudWatch Logs.

## Lambda Function Execution Role

When you create a Lambda function, you specify an execution role. The execution role grants Lambda permissions to access AWS resources that your function needs to perform its tasks. For example, if your Lambda function reads and writes data to Amazon S3 buckets or Amazon DynamoDB tables, you need to grant the function permission to access those resources. You do this by creating an IAM role and attaching policies that identify the resources that the function can access. For more information, see Creating a Role for Lambda Functions.

## Lambda Function Handler and Role

The handler is the entry point to your Lambda function. When Lambda executes your function, it passes the event data as a parameter to the handler. In return, the handler must return the data back to Lambda. The structure of the event data depends on the event source. For example, the event data from Amazon S3 contains information about the object that triggered the event, such as the file name and size. The event data from Amazon DynamoDB contains information about the item that was updated or deleted.

The handler must be a method in your code that uses the following format:

```{language}
def handler_name(event, context):
```

where handler_name is the name of the method, event is the parameter that contains the event data, and context is the parameter that contains information about the invocation, function, and execution environment.

For more information about the handler, see Lambda Function Handler in Python.

## Lambda Function Configuration

When you create or update a Lambda function, you specify function configuration information, such as the function name, description, entry point, runtime, and IAM role. You also specify the function code and any dependencies that your code requires, such as AWS SDK libraries.

## Lambda Function IAM Role

When you create a Lambda function, you specify an IAM role that Lambda uses to work with AWS resources on your behalf. For example, if your Lambda function reads and writes data to Amazon S3 buckets or Amazon DynamoDB tables, you need to grant the function permission to access those resources. You do this by creating an IAM role and attaching policies that identify the resources that the function can access. For more information, see Creating a Role for Lambda Functions.

## Lambda Function Policy

In addition to the IAM role that you specify when you create a Lambda function, Lambda also attaches a policy to the function's IAM role. The policy grants the function permission to log events to Amazon CloudWatch Logs and to write trace data to X-Ray. For more information, see Logging Lambda Function Activity to CloudWatch Logs.

## Lambda Function Execution Role

When you create a Lambda function, you specify an execution role. The execution role grants Lambda permissions to access AWS resources that your function needs to perform its tasks. For example, if your Lambda function reads and writes data to Amazon S3 buckets or Amazon DynamoDB tables, you need to grant the function permission to access those resources. You do this by creating an IAM role and attaching policies that identify the resources that the function can access. For more information, see Creating a Role for Lambda Functions.

## Lambda Function Handler and Role

The handler is the entry point to your Lambda function. When Lambda executes your function, it passes the event data as a parameter to the handler. In return, the handler must return the data back to Lambda. The structure of the event data depends on the event source. For example, the event data from Amazon S3 contains information about the object that triggered the event, such as the file name and size. The event data from Amazon DynamoDB contains information about the item that was updated or deleted.

The handler must be a method in your code that uses the following format:

```{language}
def handler_name(event, context):
```

where handler_name is the name of the method, event is the parameter that contains the event data, and context is the parameter that contains information about the invocation, function, and execution