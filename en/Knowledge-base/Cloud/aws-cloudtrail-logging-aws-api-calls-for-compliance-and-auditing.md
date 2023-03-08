---
title: AWS CloudTrail: Logging AWS API Calls for Compliance and Auditing
description: 
published: true
date: 2023-02-05T07:56:06.995Z
tags: 
editor: markdown
dateCreated: 2023-02-05T07:56:01.435Z
---

- [AWS CloudTrail: registro de llamadas a la API de AWS para cumplimiento y auditoría***Spanish** document is available*](/es/Knowledge-base/Cloud/aws-cloudtrail-logging-aws-api-calls-for-compliance-and-auditing)
{.links-list}
- [AWS CloudTrail：记录 AWS API 调用以实现合规性和审计***Chinese Simplified** document is available*](/zh/Knowledge-base/Cloud/aws-cloudtrail-logging-aws-api-calls-for-compliance-and-auditing)
{.links-list}
- [AWS CloudTrail: 규정 준수 및 감사를 위해 AWS API 호출 로깅***Korean** document is available*](/ko/Knowledge-base/Cloud/aws-cloudtrail-logging-aws-api-calls-for-compliance-and-auditing)
{.links-list}


AWS CloudTrail is a web service that records your AWS API calls and delivers log files to you. CloudTrail provides event history of your AWS account activity, including actions taken through the AWS Management Console, AWS SDKs, command line tools, and other AWS services. This event history simplifies security analysis, resource change tracking, and compliance auditing.

CloudTrail is easy to set up. You can create trails that log data to an Amazon S3 bucket, an Amazon CloudWatch Logs log group, both, or neither. You can configure multiple trails to deliver data to the same Amazon S3 bucket or Amazon CloudWatch Logs log group. When you configure AWS CloudTrail, you specify the Amazon S3 buckets or Amazon CloudWatch Logs log groups where you want CloudTrail to deliver your log files.

 Trails can log data for all AWS Regions in your AWS account, or only for selected Regions. You can enable logging for all Regions in your AWS account, or only for selected Regions. When you enable a Region for CloudTrail logging, CloudTrail creates a new trail in that Region.

## Setting up CloudTrail

To turn on logging for your AWS account, create a trail. A trail enables CloudTrail and specifies the delivery method for your CloudTrail log files. You can create a trail that logs data events for all Regions in your AWS account, or only for selected Regions. You can also configure whether the trail applies only to the resources in your AWS account, or to all AWS resources. When you've created a trail, you can view and search the log files in the AWS CloudTrail console in near real-time.

### Creating a Trail

Use the following procedure to create a trail and specify the Amazon S3 bucket or Amazon CloudWatch Logs log group where you want CloudTrail to deliver your log files.

1. Open the AWS CloudTrail console at https://console.aws.amazon.com/cloudtrail/.

2. If this is the first time you are using the AWS CloudTrail console, read the message and choose **Get Started**.

3. Choose **Create Trail**.

4. For **Name**, enter a name for the trail. The name must be unique in the region in which you are creating the trail. For example, you might name your trail MyTrail.

5. For **Apply trail to all regions**, do one of the following:

* To apply the trail to all regions, choose **Yes, apply trail to all regions**.
* To apply the trail only to selected regions, choose **No, apply trail only to the selected regions**, and then select the regions.

6. For **S3 bucket name**, enter the name of the Amazon S3 bucket where you want CloudTrail to deliver your log files. The bucket must exist in the same region where you are creating the trail. If you enter the name of an existing bucket, CloudTrail writes the log files to the bucket. If the bucket doesn't exist, CloudTrail creates the bucket.

7. For **S3 key prefix**, enter an optional prefix for the log file names. If you don't specify a prefix, the log files are delivered without a prefix.

8. For **CloudWatch Logs log group name**, enter the name of the Amazon CloudWatch Logs log group where you want CloudTrail to deliver your log files. The log group must exist in the same region where you are creating the trail.

9. For **Enable log file validation**, do one of the following:

* To create digital signatures for all log files, choose **Yes**. CloudTrail creates digital signatures for all log files.
* To opt out of digital signatures for all log files, choose **No**.

10. Choose **Create**.

After you create a trail, you need to set up Amazon S3 to publish events to the trail.

### Setting up Amazon S3

When you create a trail, you specify the Amazon S3 bucket where you want CloudTrail to deliver your log files. CloudTrail uses Amazon S3 to send log files from each Region in your AWS account. You need to set up Amazon S3 to publish events to the trail.

1. Open the Amazon S3 console at https://console.aws.amazon.com/s3/.

2. In the Amazon S3 console, choose the name of the bucket that you specified when you created the trail.

3. Choose **Properties**.

4. In the Properties pane, choose **Events**.

5. Choose **Add notification**.

6. In the **Name** field, enter a name for the event.

7. For **Events**, choose **All object create events**.

8. For **Send to**, choose **SNS Topic**.

9. For **SNS Topic ARN**, enter the ARN for the Amazon SNS topic that you specified when you created the trail.

10. Choose **Save**.

After you set up Amazon S3 to publish events to the trail, CloudTrail starts logging AWS API calls for the resources in the bucket that you specified. It can take up to 15 minutes for CloudTrail to deliver the log files to the bucket.

## Viewing Log Files

After you create a trail and set up Amazon S3 to publish events, you can view and search the log files in the AWS CloudTrail console in near real-time.

1. Open the AWS CloudTrail console at https://console.aws.amazon.com/cloudtrail/.

2. Choose **Trails**.

3. Choose the name of the trail.

4. On the **Configure trail** page, choose **View log files**.

5. In the **Log files** list, choose the name of a log file.

6. Choose **Download**.

7. In the **Download log file** dialog box, choose **Save file**.

## CloudTrail Log File Format

CloudTrail log files contain one or more log entries. A log entry represents a single request from any source and includes information about the requested action, the date and time of the action, request parameters, and so on.

CloudTrail writes log entries to log files using a space-delimited format. Each log entry consists of nine fields that are separated by spaces. The fields enable you to reconstruct and understand the sequence of events that occurred, including which user or role initiated the event, when the event occurred, which resources were affected, and so on.

The following table describes the fields in a CloudTrail log entry.

| Field | Description |
| --- | --- |
| **eventID** | A unique identifier for the event. For example, **eventID=55746930-A87B-4E50-95A7-12B80B6E8700**. |
| **eventName** | The name of the event. For example, **eventName=RunInstances**. |
| **eventSource** | The AWS service that generated the event. For example, **eventSource=ec2.amazonaws.com** or **eventSource=iam.amazonaws.com**. |
| **awsRegion** | The AWS Region where the event occurred. For example, **awsRegion=us-east-1**. |
| **sourceIPAddress** | The IP address of the requester. |
| **userAgent** | The user agent information included in the request, if any. |
| **requestParameters** | Any request parameters included in the event, if any. Request parameters are typically included for actions taken through the AWS Management Console or the AWS API. The format for request parameters depends on the **eventName**. |
| **responseElements** | The response elements returned by the AWS service, if any. Response elements are typically included for actions taken through the AWS Management Console. The format for response elements depends on the **eventName**. |
| **additionalEventData** | Additional information about the event. |
| **requestID** | A value that identifies the request. |
| **eventType** | The type of the event. Valid values are **AwsApiCall**, **AwsServiceEvent**, and **AwsSdkCall**. |
| **recipientAccountId** | The AWS account ID that receives events from another AWS account. For example, events from a member account in an organization are delivered to the master account. This field is only populated for cross-account events. |
| **sharedEventId** | The **eventID** of the event in the master account. This field is only populated for cross-account events. |

## CloudTrail Log File Example

The following is an example of a CloudTrail log file.

```
55746930-A87B-4E50-95A7-12B80B6E8700 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Mozilla/5.0 aws-cli/1.7.28 Python/2.7.9 Windows/2012server botocore/1.3.22
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 RunInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User-Agent=Console aws-cli/1.7.11 Python/2.7.9 Windows/7 SP1 botocore/1.3.11
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 User