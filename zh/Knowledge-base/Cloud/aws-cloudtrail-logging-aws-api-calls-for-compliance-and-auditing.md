---
title: AWS CloudTrail：记录 AWS API 调用以实现合规性和审计
description: 
published: true
date: 2023-02-05T07:56:03.107Z
tags: 
editor: markdown
dateCreated: 2023-02-05T07:56:01.423Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [AWS CloudTrail: Logging AWS API Calls for Compliance and Auditing***English** document is available*](/en/Knowledge-base/Cloud/aws-cloudtrail-logging-aws-api-calls-for-compliance-and-auditing)
{.links-list}


AWS CloudTrail 是一种 Web 服务，可记录您的 AWS API 调用并向您提供日志文件。 CloudTrail 提供您的 AWS 账户活动的事件历史记录，包括通过 AWS 管理控制台、AWS SDK、命令行工具和其他 AWS 服务执行的操作。此事件历史记录简化了安全分析、资源更改跟踪和合规性审计。

CloudTrail 易于设置。您可以创建跟踪，将数据记录到 Amazon S3 存储桶、Amazon CloudWatch Logs 日志组，或者两者都记录。您可以配置多个跟踪以将数据传送到同一个 Amazon S3 存储桶或 Amazon CloudWatch Logs 日志组。当您配置 AWS CloudTrail 时，您可以指定您希望 CloudTrail 将日志文件传送到的 Amazon S3 存储桶或 Amazon CloudWatch Logs 日志组。

 Trails 可以记录您 AWS 账户中所有 AWS 区域的数据，或仅记录选定区域的数据。您可以为您的 AWS 账户中的所有区域启用日志记录，或仅为选定区域启用日志记录。当您为 CloudTrail 日志记录启用区域时，CloudTrail 会在该区域中创建一个新跟踪。

## 设置 CloudTrail

要为您的 AWS 账户打开日志记录，请创建一个跟踪。跟踪启用 CloudTrail 并指定 CloudTrail 日志文件的传送方法。您可以创建一个跟踪来记录您 AWS 账户中所有区域的数据事件，或仅记录选定区域的数据事件。您还可以配置跟踪是仅应用于您的 AWS 账户中的资源，还是应用于所有 AWS 资源。创建跟踪后，您可以在 AWS CloudTrail 控制台中近乎实时地查看和搜索日志文件。

### 创建轨迹

使用以下过程创建跟踪并指定您希望 CloudTrail 将日志文件传送到的 Amazon S3 存储桶或 Amazon CloudWatch Logs 日志组。

1. 在 https://console.aws.amazon.com/cloudtrail/ 打开 AWS CloudTrail 控制台。

2. 如果这是您第一次使用 AWS CloudTrail 控制台，请阅读消息并选择 **Get Started**。

3. 选择**创建轨迹**。

4. 对于**名称**，输入路径的名称。该名称在您创建跟踪的区域中必须是唯一的。例如，您可以将跟踪命名为 MyTrail。

5. 对于 **Apply trail to all regions**，执行以下操作之一：

* 要将跟踪应用于所有区域，请选择**是，将跟踪应用于所有区域**。
* 要仅将轨迹应用于选定区域，请选择**否，仅将轨迹应用于选定区域**，然后选择区域。

6. 对于 **S3 存储桶名称**，输入您希望 CloudTrail 将日志文件传送到的 Amazon S3 存储桶的名称。存储桶必须存在于您创建跟踪的同一区域中。如果您输入现有存储桶的名称，CloudTrail 会将日志文件写入该存储桶。如果存储桶不存在，CloudTrail 会创建该存储桶。

7. 对于 **S3 密钥前缀**，输入日志文件名的可选前缀。如果您不指定前缀，则日志文件将在没有前缀的情况下传送。

8. 对于**CloudWatch Logs 日志组名称**，输入您希望 CloudTrail 将日志文件传送到的 Amazon CloudWatch Logs 日志组的名称。日志组必须存在于您创建跟踪的同一区域中。

9. 对于 **启用日志文件验证**，执行以下操作之一：

* 要为所有日志文件创建数字签名，请选择**是**。 CloudTrail 为所有日志文件创建数字签名。
* 要选择退出所有日志文件的数字签名，请选择 **否**。

10. 选择**创建**。

创建跟踪后，您需要设置 Amazon S3 以将事件发布到跟踪。

### 设置亚马逊 S3

创建跟踪时，您可以指定希望 CloudTrail 将日志文件传送到的 Amazon S3 存储桶。 CloudTrail 使用 Amazon S3 从您的 AWS 账户中的每个区域发送日志文件。您需要设置 Amazon S3 以将事件发布到跟踪。

1. 在 https://console.aws.amazon.com/s3/ 打开 Amazon S3 控制台。

2. 在 Amazon S3 控制台中，选择您在创建跟踪时指定的存储桶的名称。

3. 选择**属性**。

4. 在“属性”窗格中，选择“**事件**”。

5. 选择**添加通知**。

6. 在**名称**字段中，输入事件的名称。

7. 对于**事件**，选择**所有对象创建事件**。

8. 对于 **Send to**，选择 **SNS Topic**。

9. 对于 **SNS 主题 ARN**，输入您在创建跟踪时指定的 Amazon SNS 主题的 ARN。

10. 选择**保存**。

在您设置 Amazon S3 以将事件发布到跟踪后，CloudTrail 开始记录对您指定的存储桶中的资源的 AWS API 调用。 CloudTrail 最多可能需要 15 分钟才能将日志文件传送到存储桶。

## 查看日志文件

创建跟踪并设置 Amazon S3 以发布事件后，您可以在 AWS CloudTrail 控制台中近乎实时地查看和搜索日志文件。

1. 在 https://console.aws.amazon.com/cloudtrail/ 打开 AWS CloudTrail 控制台。

2. 选择**轨迹**。

3. 选择路径名称。

4. 在 **Configure trail** 页面上，选择 **View log files**。

5. 在**日志文件**列表中，选择日志文件的名称。

6. 选择**下载**。

7. 在**下载日志文件**对话框中，选择**保存文件**。

## CloudTrail 日志文件格式

CloudTrail 日志文件包含一个或多个日志条目。日志条目表示来自任何来源的单个请求，包括有关请求的操作、操作的日期和时间、请求参数等的信息。

CloudTrail 使用以空格分隔的格式将日志条目写入日志文件。每个日志条目由九个字段组成，这些字段由空格分隔。这些字段使您能够重建和理解事件发生的顺序，包括哪个用户或角色发起了事件、事件发生的时间、哪些资源受到影响等等。

下表描述了 CloudTrail 日志条目中的字段。

|领域 |说明 |
| --- | --- |
| **事件ID** |事件的唯一标识符。例如，**eventID=55746930-A87B-4E50-95A7-12B80B6E8700**。 |
| **事件名称** |事件的名称。例如，**eventName=RunInstances**。 |
| **事件源** |生成事件的 AWS 服务。例如，**eventSource=ec2.amazonaws.com** 或 **eventSource=iam.amazonaws.com**。 |
| **aws区域** |事件发生的 AWS 区域。例如，**awsRegion=us-east-1**。 |
| **源IP地址** |请求者的 IP 地址。 |
| **用户代理** |请求中包含的用户代理信息（如果有）。 |
| **请求参数** |事件中包含的任何请求参数（如果有）。请求参数通常包含在通过 AWS 管理控制台或 AWS API 执行的操作中。请求参数的格式取决于**eventName**。 |
| **响应元素** | AWS 服务返回的响应元素（如果有）。通过 AWS 管理控制台执行的操作通常包括响应元素。响应元素的格式取决于 **eventName**。 |
| **附加事件数据** |有关该事件的其他信息。 |
| **请求ID** |标识请求的值。 |
| **事件类型** |事件的类型。有效值为 **AwsApiCall**、**AwsServiceEvent** 和 **AwsSdkCall**。 |
| **收件人帐号** |从另一个 AWS 账户接收事件的 AWS 账户 ID。例如，来自组织中成员账户的事件被传送到主账户。此字段仅为跨账户事件填充。 |
| **sharedEventId** |主账户中事件的 **eventID**。此字段仅为跨账户事件填充。 |

## CloudTrail 日志文件示例

以下是 CloudTrail 日志文件的示例。

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
54e3d16e-aae8-11e4-bfdb-c81f66cc4da7 DescribeInstances ec2.amazonaws.com us-east-1 1.2.3.4 用户