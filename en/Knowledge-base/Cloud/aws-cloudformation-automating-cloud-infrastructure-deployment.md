---
title: AWS CloudFormation: Automating Cloud Infrastructure Deployment
description: 
published: true
date: 2023-02-19T02:32:55.830Z
tags: 
editor: markdown
dateCreated: 2023-02-19T02:32:48.973Z
---

- [AWS CloudFormation: 클라우드 인프라 배포 자동화***Korean** document is available*](/ko/Knowledge-base/Cloud/aws-cloudformation-automating-cloud-infrastructure-deployment)
{.links-list}


# AWS CloudFormation: Automating Cloud Infrastructure Deployment

CloudFormation is a powerful AWS service that allows developers to automate the creation and deployment of cloud infrastructure. In this article, we will take a closer look at what CloudFormation is and how it can be used to simplify the process of provisioning and managing cloud resources.

## What is CloudFormation?

CloudFormation is a service that allows developers to define and provision cloud infrastructure using templates written in JSON or YAML. Once a template has been defined, CloudFormation can be used to create, update, and delete a stack of resources based on that template.

One of the benefits of using CloudFormation is that it allows for infrastructure to be defined as code. This means that infrastructure can be versioned, tracked, and automated just like any other code resource.

Another benefit of CloudFormation is that it can be used to provision resources across multiple AWS accounts and regions. This can be helpful when managing resources for development, testing, and production environments.

## CloudFormation Template Basics

A CloudFormation template is a JSON or YAML document that defines a stack of AWS resources. A template can include multiple resources, each of which can be defined using either a simple or nested format.

A simple format resource is defined by a single JSON or YAML object. This object must include a Type property that specifies the type of resource to be created, and a Properties property that defines the resource's properties.

A nested format resource is defined by a JSON or YAML object that includes a Type property and a Properties property, as well as a NestedStackId property. The NestedStackId property contains the stack ID of a nested stack, which is a stack that is created within another stack.

## Creating a CloudFormation Stack

Once a CloudFormation template has been defined, it can be used to create a new stack. To create a stack, you must specify a stack name, a template URL, and a set of parameters.

The stack name is used to uniquely identify the stack. The template URL is the location of the template file. The template file can be stored in an Amazon S3 bucket, or it can be inline.

The parameters are a set of key-value pairs that are used to configure the stack. The keys must be specified in the template, and the values must be provided when the stack is created.

Once the stack has been created, CloudFormation will provision the resources that are defined in the template. This process can take a few minutes to complete.

## Updating a CloudFormation Stack

Once a stack has been created, it can be updated. To update a stack, you must specify a new template URL and a set of parameters.

When you update a stack, CloudFormation will first compare the new template to the existing template. If there are no changes, CloudFormation will do nothing. If there are changes, CloudFormation will update the stack.

## Deleting a CloudFormation Stack

Once a stack is no longer needed, it can be deleted. Deleting a stack will delete all of the resources that are defined in the stack.

## CloudFormation Use Cases

CloudFormation can be used to provision nearly any type of AWS resource. Some common use cases for CloudFormation include:

- Creating a virtual private cloud (VPC)
- Launching an Amazon EC2 instance
- Creating an Amazon RDS database
- Creating an Amazon S3 bucket

## CloudFormation Template Examples

Here are a few examples of CloudFormation templates that can be used to provision common AWS resources.

### Creating a VPC

This template can be used to create a VPC with a public and private subnet.

```yaml
AWSTemplateFormatVersion: 2010-09-09

Description: A VPC with a public and private subnet.

Parameters:

  VpcCidr:
    Description: The CIDR block for the VPC.
    Type: String
    Default: 172.16.0.0/16

  PublicSubnet1Cidr:
    Description: The CIDR block for the public subnet.
    Type: String
    Default: 172.16.0.0/24

  PrivateSubnet1Cidr:
    Description: The CIDR block for the private subnet.
    Type: String
    Default: 172.16.1.0/24

Resources:

  Vpc:
    Type: AWS::EC2::VPC
    Properties:
      CidrBlock: !Ref VpcCidr
      InstanceTenancy: default

  PublicSubnet1:
    Type: AWS::EC2::Subnet
    Properties:
      VpcId: !Ref Vpc
      CidrBlock: !Ref PublicSubnet1Cidr
      AvailabilityZone: us-east-1a

  PrivateSubnet1:
    Type: AWS::EC2::Subnet
    Properties:
      VpcId: !Ref Vpc
      CidrBlock: !Ref PrivateSubnet1Cidr
      AvailabilityZone: us-east-1a
```

### Creating an EC2 Instance

This template can be used to launch an EC2 instance.

```yaml
AWSTemplateFormatVersion: 2010-09-09

Description: A simple EC2 instance.

Parameters:

  KeyName:
    Description: The name of the SSH key pair to use.
    Type: String

  InstanceType:
    Description: The type of EC2 instance to launch.
    Type: String
    Default: t2.micro

  ImageId:
    Description: The ID of the AMI to use.
    Type: String

Resources:

  Ec2Instance:
    Type: AWS::EC2::Instance
    Properties:
      KeyName: !Ref KeyName
      InstanceType: !Ref InstanceType
      ImageId: !Ref ImageId
```

### Creating an RDS Database

This template can be used to create an RDS database.

```yaml
AWSTemplateFormatVersion: 2010-09-09

Description: A simple RDS database.

Parameters:

  DbInstanceIdentifier:
    Description: The database instance identifier.
    Type: String

  DbInstanceClass:
    Description: The database instance class.
    Type: String
    Default: db.t2.micro

  DbName:
    Description: The database name.
    Type: String

Resources:

  DbInstance:
    Type: AWS::RDS::DBInstance
    Properties:
      DbInstanceIdentifier: !Ref DbInstanceIdentifier
      DbInstanceClass: !Ref DbInstanceClass
      Engine: MySQL
      MasterUsername: root
      MasterUserPassword: password
      AllocatedStorage: 5
      DbName: !Ref DbName
```

### Creating an S3 Bucket

This template can be used to create an S3 bucket.

```yaml
AWSTemplateFormatVersion: 2010-09-09

Description: A simple S3 bucket.

Parameters:

  BucketName:
    Description: The name of the S3 bucket.
    Type: String

Resources:

  Bucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: !Ref BucketName
```

## Conclusion

CloudFormation is a powerful AWS service that allows developers to automate the creation and deployment of cloud infrastructure. In this article, we took a closer look at what CloudFormation is and how it can be used to simplify the process of provisioning and managing cloud resources.