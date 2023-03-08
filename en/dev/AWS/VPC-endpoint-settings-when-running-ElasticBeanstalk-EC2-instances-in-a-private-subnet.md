---
title: VPC endpoint settings when running ElasticBeanstalk EC2 instances in a private subnet
description: 
published: true
date: 2023-02-17T18:00:24.285Z
tags: aws, ec2, elasticbeanstalk, english, vpc
editor: markdown
dateCreated: 2022-12-24T20:55:11.583Z
---

- [ElasticBeanstalk EC2 인스턴스를 private subnet 에서 실행시 VPC endpoint 설정***Korean** version of this document is available*](/ko/dev/AWS/VPC-endpoint-settings-when-running-ElasticBeanstalk-EC2-instances-in-a-private-subnet)
{.links-list}

> I did a lot of shoveling to create a custom VPC and run ElasticBeanstalk EC2 instances in a private subnet.
> Make a note of it to avoid future mistakes.
{.is-info}

# Configuring ElasticBeanstalk

- **Public subnet**
   - Load Balancer
- **Private subnet**
   - EC2 (Network - Public IP allocation off)
  
# VPC endpoint configuration

- Additional configuration is required so that ElasticBeanstalk EC2 instances in the private subnet can communicate with AWS services. (It would be nice to check this in the VPC creation wizard, but it doesn't)
- The endpoints below must be created to connect to all private subents set in the VPC.
   - `com.amazonaws.{region}.elasticbeanstalk`
   - `com.amazonaws.{region}.elasticbeanstalk-health` (if using Enhanced Log)
   - `com.amazonaws.{region}.cloudformation`
   - `com.amazonaws.{region}.ecr.api` (if using ECR)
   - `com.amazonaws.{region}.ecr.dkr` (if using ECR)
   - `com.amazonaws.{region}.logs` (CloudWatch)
   - `com.amazonaws.{region}.s3` (both Gateway / Interface)
   - `com.amazonaws.{region}.sqs`
- When creating the above endpoint, all `Private DNS` settings must be checked. (Excluding S3 Interface)
- Services that are not actually used may have been added. It doesn't seem to matter anyway.
- There is no need to set up a separate Routing Table.

# References

- [Things to know when using Elastic Beanstalk in a VPC environment*YOWU DEV WIKI*](/en/dev/AWS/Things-to-know-when-using-Elastic-Beanstalk-in-a-VPC-environment)
- [Using Elastic Beanstalk with Amazon VPC*AWS Documents*](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/vpc.html#services-vpc-private-beanstalk)
{.links-list}