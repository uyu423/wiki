---
title: Building Hybrid Clouds with AWS and Azure
description: 
published: true
date: 2023-02-17T18:12:09.142Z
tags: 
editor: markdown
dateCreated: 2023-01-30T19:04:19.546Z
---

- [AWS 및 Azure로 하이브리드 클라우드 구축***Korean** version of this document is available*](/ko/Knowledge-base/Cloud/building-hybrid-clouds-with-aws-and-azure)
{.links-list}
- [AWS と Azure を使用したハイブリッド クラウドの構築***Japanese** version of this document is available*](/ja/Knowledge-base/Cloud/building-hybrid-clouds-with-aws-and-azure)
{.links-list}
- [使用 AWS 和 Azure 构建混合云***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Cloud/building-hybrid-clouds-with-aws-and-azure)
{.links-list}




# Building Hybrid Clouds with AWS and Azure

With the recent releases of Azure Stack and AWS Outposts, it's now possible to build hybrid clouds that span both Azure and AWS. In this article, we'll take a look at how to do this, and some of the benefits and drawbacks of doing so.

## What is a Hybrid Cloud?

A hybrid cloud is a type of cloud computing that uses a mix of on-premises and cloud-based resources. This can be a mix of public and private clouds, or a mix of different cloud providers.

One common use case for a hybrid cloud is to use the cloud for compute and storage resources, while keeping data on-premises for security or regulatory reasons.

Another common use case is to use the cloud for development and test, while keeping production on-premises. This can be done for cost reasons, or to keep production data on a more secure network.

## Azure Stack and AWS Outposts

Azure Stack is an on-premises version of Azure, that can be used to build hybrid clouds. It includes all of the same compute, storage, and networking resources as Azure, and can be managed using the same Azure portal.

AWS Outposts is an on-premises version of AWS, that can be used to build hybrid clouds. It includes all of the same compute, storage, and networking resources as AWS, and can be managed using the same AWS console.

## Building a Hybrid Cloud

There are two main ways to build a hybrid cloud with Azure and AWS:

### Option 1: Use Azure Stack for Compute and AWS Outposts for Storage

In this option, you would use Azure Stack for all of your compute resources, and AWS Outposts for all of your storage resources. Your data would be stored in S3 buckets on Outposts, and you would access it from your applications running on Azure Stack.

One benefit of this option is that you would only need to manage one set of resources. All of your compute would be managed in the Azure portal, and all of your storage would be managed in the AWS console.

A drawback of this option is that it would not be possible to take advantage of Azure's blob storage, or AWS's EBS volumes. You would also need to have Outposts installed in the same location as your Azure Stack deployment.

### Option 2: Use Azure Stack for Storage and AWS Outposts for Compute

In this option, you would use Azure Stack for all of your storage resources, and AWS Outposts for all of your compute resources. Your data would be stored in blob storage on Azure Stack, and you would access it from your applications running on AWS Outposts.

One benefit of this option is that you could take advantage of Azure's blob storage. This could be used for data that is accessed infrequently, or for data that needs to be stored in a secure location.

A drawback of this option is that it would not be possible to take advantage of AWS's EBS volumes. You would also need to have Outposts installed in the same location as your Azure Stack deployment.

## Conclusion

Building a hybrid cloud with Azure and AWS is a great way to take advantage of the best of both worlds. Azure Stack and AWS Outposts make it easy to deploy and manage your hybrid cloud.