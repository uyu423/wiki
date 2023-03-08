---
title: AWS Direct Connect: Building High-Speed Network Connections to the Cloud
description: 
published: true
date: 2023-02-06T03:55:16.850Z
tags: 
editor: markdown
dateCreated: 2023-02-06T03:55:15.279Z
---

- [AWS Direct Connect: Creación de conexiones de red de alta velocidad a la nube***Spanish** document is available*](/es/Knowledge-base/Cloud/aws-direct-connect-building-high-speed-network-connections-to-the-cloud)
{.links-list}
- [AWS Direct Connect：建立与云的高速网络连接***Chinese Simplified** document is available*](/zh/Knowledge-base/Cloud/aws-direct-connect-building-high-speed-network-connections-to-the-cloud)
{.links-list}
- [AWS Direct Connect: 클라우드에 대한 고속 네트워크 연결 구축***Korean** document is available*](/ko/Knowledge-base/Cloud/aws-direct-connect-building-high-speed-network-connections-to-the-cloud)
{.links-list}


# AWS Direct Connect: Building High-Speed Network Connections to the Cloud

## Introduction

AWS Direct Connect lets you establish a private network connection from your on-premises environment to your Amazon Virtual Private Cloud (Amazon VPC). Using AWS Direct Connect, you can create virtual interfaces directly to AWS, which can provide improved performance, security, and reliability compared to Internet-based connections.

AWS Direct Connect is available in select AWS Regions only. You can choose to connect to the AWS Region that provides the lowest cost or latencies for your applications.

## Creating a Connection

You can create an AWS Direct Connect connection in one of two ways:

-   Using the AWS Management Console

-   Using the AWS Command Line Interface (AWS CLI)

## Configuring a Connection

After you've created a connection, you must configure it before you can use it. You can do this using the AWS Management Console or the AWS CLI.

## Using AWS Direct Connect

Once you've created and configured your connection, you can begin using it to establish a private network connection between your on-premises environment and your Amazon VPC.

You can use AWS Direct Connect in one of two ways:

-   With public virtual interfaces, to connect to Amazon CloudFront, Amazon Route 53, or Amazon S3

-   With private virtual interfaces, to connect to Amazon Elastic Compute Cloud (Amazon EC2), Amazon Simple Storage Service (Amazon S3), Amazon DynamoDB, or Amazon Virtual Private Cloud (Amazon VPC)

## Pricing

AWS Direct Connect pricing is based on two components:

-   The connection rate, which is the speed of your connection

-   The monthly port fee