---
title: AWS IAM: Managing User Access and Permissions in the Cloud
description: 
published: true
date: 2023-01-31T08:43:46.403Z
tags: 
editor: markdown
dateCreated: 2023-01-31T08:43:42.835Z
---

- [AWS IAM: 클라우드에서 사용자 액세스 및 권한 관리***Korean** version of this document is available*](/ko/Knowledge-base/Cloud/aws-iam-managing-user-access-and-permissions-in-the-cloud)
{.links-list}
- [AWS IAM: クラウドでのユーザー アクセスとアクセス許可の管理***Japanese** version of this document is available*](/ja/Knowledge-base/Cloud/aws-iam-managing-user-access-and-permissions-in-the-cloud)
{.links-list}
- [AWS IAM：管理云中的用户访问和权限***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Cloud/aws-iam-managing-user-access-and-permissions-in-the-cloud)
{.links-list}



# AWS IAM: Managing User Access and Permissions in the Cloud

Developers and operators who are responsible for managing user access and permissions in the cloud need to be aware of the different tools and services that are available to them. This article provides an overview of the AWS Identity and Access Management (IAM) service and how it can be used to manage user access and permissions in the cloud.

## What is AWS IAM?

AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources. IAM is a feature of your AWS account that is separate from the resources themselves. IAM allows you to create and manage users and groups, and use permissions to allow and deny their access to AWS resources.

IAM is a universal service that is not specific to any one region. It is globally available in all AWS regions.

## How does AWS IAM work?

AWS IAM consists of the following components:

-   **Users**: IAM users are AWS accounts that are used to access AWS resources. IAM users are different from the AWS accounts that are used to access the AWS Management Console. IAM users are not given any permissions by default. You must explicitly grant permissions to IAM users.

-   **Groups**: IAM groups are collections of IAM users. Groups are a way to manage multiple IAM users at once. IAM groups can be used to specify permissions for multiple users, which can be useful if you have a large number of users or if you often need to change the permissions for a large number of users.

-   **Policies**: IAM policies are documents that specify which actions an IAM user or group is allowed to perform on which AWS resources. IAM policies are written in JSON.

-   **Roles**: IAM roles are a way to delegate access to AWS resources to entities that you trust. Roles are used to grant permissions to IAM users or groups that you do not trust with your AWS credentials. Roles can also be used to grant permissions to AWS services that need to access your resources, such as Amazon S3 or Amazon DynamoDB.

IAM is a universal service, meaning that it is not specific to any one region. It is globally available in all AWS regions.

## Creating IAM Users

IAM users are AWS accounts that are used to access AWS resources. IAM users are different from the AWS accounts that are used to access the AWS Management Console. IAM users are not given any permissions by default. You must explicitly grant permissions to IAM users.

To create an IAM user, you must first create an IAM group. IAM groups are collections of IAM users. IAM groups can be used to specify permissions for multiple users, which can be useful if you have a large number of users or if you often need to change the permissions for a large number of users.

Once you have created an IAM group, you can add IAM users to the group. To add an IAM user to a group, you must have the iam:AddUserToGroup permission.

## Attaching Policies to IAM Users

Policies are documents that specify which actions an IAM user or group is allowed to perform on which AWS resources. IAM policies are written in JSON.

You can attach policies to IAM users in two ways:

-   You can inline the policy in the user's data.
-   You can create a policy and then attach it to the user.

Policies can be attached to multiple users and groups.

## Creating IAM Roles

IAM roles are a way to delegate access to AWS resources to entities that you trust. Roles are used to grant permissions to IAM users or groups that you do not trust with your AWS credentials. Roles can also be used to grant permissions to AWS services that need to access your resources, such as Amazon S3 or Amazon DynamoDB.

To create an IAM role, you must first create an IAM policy. IAM policies are documents that specify which actions an IAM user or group is allowed to perform on which AWS resources. IAM policies are written in JSON.

Once you have created an IAM policy, you can create an IAM role and attach the policy to the role.

Roles can be attached and detached from IAM users and groups.

## Deleting IAM Users

IAM users can be deleted at any time. When an IAM user is deleted, all of the user's permissions are also deleted. Deleting an IAM user does not delete the AWS resources that the user has access to.

To delete an IAM user, you must have the iam:DeleteUser permission.

## Summary

AWS Identity and Access Management (IAM) is a web service that helps you securely control access to AWS resources. IAM is a feature of your AWS account that is separate from the resources themselves. IAM allows you to create and manage users and groups, and use permissions to allow and deny their access to AWS resources.

IAM is a universal service that is not specific to any one region. It is globally available in all AWS regions.

IAM users are AWS accounts that are used to access AWS resources. IAM users are different from the AWS accounts that are used to access the AWS Management Console. IAM users are not given any permissions by default. You must explicitly grant permissions to IAM users.

IAM groups are collections of IAM users. IAM groups can be used to specify permissions for multiple users, which can be useful if you have a large number of users or if you often need to change the permissions for a large number of users.

Policies are documents that specify which actions an IAM user or group is allowed to perform on which AWS resources. IAM policies are written in JSON.

IAM roles are a way to delegate access to AWS resources to entities that you trust. Roles are used to grant permissions to IAM users or groups that you do not trust with your AWS credentials. Roles can also be used to grant permissions to AWS services that need to access your resources, such as Amazon S3 or Amazon DynamoDB.

IAM is a universal service, meaning that it is not specific to any one region. It is globally available in all AWS regions.