---
title: AWS SES: Sending and Receiving Emails with Simple Email Service
description: 
published: true
date: 2023-02-17T18:14:48.823Z
tags: 
editor: markdown
dateCreated: 2023-01-30T21:57:30.664Z
---

- [AWS SES: 간단한 이메일 서비스로 이메일 보내기 및 받기***Korean** version of this document is available*](/ko/Knowledge-base/Cloud/aws-ses-sending-and-receiving-emails-with-simple-email-service)
{.links-list}
- [AWS SES: Simple Email Service を使用した E メールの送受信***Japanese** version of this document is available*](/ja/Knowledge-base/Cloud/aws-ses-sending-and-receiving-emails-with-simple-email-service)
{.links-list}
- [AWS SES：使用简单的电子邮件服务发送和接收电子邮件***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Cloud/aws-ses-sending-and-receiving-emails-with-simple-email-service)
{.links-list}


# AWS SES: Sending and Receiving Emails with Simple Email Service

Welcome to the IT Development Learning Blog. In this article, we'll be discussing how to use AWS Simple Email Service to send and receive emails. 

## What is AWS Simple Email Service?

AWS Simple Email Service (SES) is a cost-effective and flexible way to send and receive emails. It's a cloud-based email service that enables you to send and receive email using your own domain name, and it supports both personal and corporate use cases. 

AWS SES is a reliable and scalable email service that integrates with other AWS services. It offers a pay-as-you-go pricing model with no upfront costs, and it's easy to set up and use. 

## Sending Emails with AWS SES

To send an email using AWS SES, you need to have an AWS account and a verified email address or domain. If you don't have an AWS account yet, you can create one [here](https://aws.amazon.com/). 

Once you have an AWS account, you can [verify an email address](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/verify-email-addresses.html) or [domain](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/verify-domains.html) with AWS SES. After you verify an email address or domain, you can start sending emails. 

You can send emails using the AWS SES console, the AWS SES API, or the AWS Command Line Interface (CLI). In this article, we'll be using the AWS SES console to send an email. 

First, go to the AWS SES console and choose **Email Addresses** from the menu. Then, choose **Verify a New Email Address** and enter the email address you want to verify. 

![Verify Email Address](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/01-verify-email-address.png)

AWS SES will send a verification email to the address you entered. Follow the instructions in the verification email to complete the verification process. 

Now that you've verified your email address, you're ready to send your first email. Go to the **AWS SES console** and choose **Send a Single Email**. 

![Send a Single Email](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/02-send-email.png)

On the **Send a Single Email** page, enter the following information: 

* **From**: Enter the verified email address that you want to use to send the email. 
* **To**: Enter the email address of the recipient. 
* **Subject**: Enter a subject for the email. 
* **Message**: Enter the body of the email. You can use the **Visual Editor** or the **HTML Editor** to format the email. 

When you're done, choose **Send Email**. 

![Send Email](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/03-send-email.png)

You should receive a confirmation email from AWS SES when the email is sent successfully. 

## Receiving Emails with AWS SES

In addition to sending emails, you can also use AWS SES to receive emails. You can use AWS SES to receive emails in your mailbox or route incoming emails to other AWS services, such as Amazon S3 or Amazon Lambda. 

To set up email receiving, you first need to [set up a rule set](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/receiving-email-getting-started.html) in the AWS SES console. A rule set consists of one or more rules that determine how AWS SES processes incoming emails. 

![Rule Sets](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/04-rule-sets.png)

To set up a rule set, choose **Rule Sets** from the menu and then choose **Create a Rule Set**. On the **Create a Rule Set** page, enter a name for the rule set and choose **Create Rule Set**. 

![Create Rule Set](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/05-create-rule-set.png)

Once the rule set is created, you can add rules to it. A rule consists of a set of conditions and an actions. When an incoming email meets the conditions of a rule, the action is executed. 

To add a rule to the rule set, choose **Add Rule** and enter the following information: 

* **Name**: Enter a name for the rule. 
* **Description**: Enter a description for the rule. 
* **Scope**: Choose whether the rule applies to all emails or only to emails that meet specific conditions. 
* **Recipient**: Enter the email address that you want to receive the email. 
* **Actions**: Choose the action that you want AWS SES to take when the rule is triggered. You can choose to save the email to an Amazon S3 bucket, send it to an Amazon Lambda function, or forward it to another email address. 

When you're done, choose **Create Rule**. 

![Create Rule](https://github.com/chatgpt/articles/raw/master/aws-ses-sending-receiving-emails/images/06-create-rule.png)

Now that you've created a rule set and added a rule to it, you're ready to receive emails. To test your setup, send an email to the email address you specified in the rule. You should receive the email in your mailbox or the Amazon S3 bucket you specified. 

## Conclusion

In this article, we've discussed how to use AWS Simple Email Service to send and receive emails. We've also shown how to set up a rule set to process incoming emails. 

AWS SES is a cost-effective and scalable way to send and receive emails. It's easy to set up and use, and it integrates with other AWS services. If you need to send or receive emails in your application, we recommend using AWS SES. 

## Additional Resources

If you want to learn more about AWS SES, we recommend the following resources: 

* [AWS SES Developer Guide](https://docs.aws.amazon.com/ses/latest/DeveloperGuide/Welcome.html)
* [Sending Email with Amazon SES](https://aws.amazon.com/ses/sending-email/)
* [Receiving Email with Amazon SES](https://aws.amazon.com/ses/receiving-email/)