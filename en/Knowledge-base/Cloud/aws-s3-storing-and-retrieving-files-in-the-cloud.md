---
title: AWS S3: Storing and Retrieving Files in the Cloud
description: 
published: true
date: 2023-02-19T01:32:48.581Z
tags: 
editor: markdown
dateCreated: 2023-02-19T01:32:41.738Z
---

- [AWS S3: 클라우드에서 파일 저장 및 검색***Korean** document is available*](/ko/Knowledge-base/Cloud/aws-s3-storing-and-retrieving-files-in-the-cloud)
{.links-list}


# AWS S3: Storing and Retrieving Files in the Cloud

Amazon Simple Storage Service (S3) is an object storage service that offers industry-leading scalability, data availability, security, and performance. This means that you can use S3 to store and retrieve any amount of data, at any time, from anywhere on the web.

S3 is designed to make web-scale computing easier for developers. It is a simple web service interface that you can use to store and retrieve any amount of data, at any time, from anywhere on the Internet. S3 is an inexpensive way to store data for highly available and scalable applications.

## What is an Object?

In Amazon S3, an object is a file, and every object has a key (a name) and a value (the data that the file contains). Object values can range from a few kilobytes to a maximum of 5 terabytes. Objects are stored in buckets, and every object must reside in a bucket.

A typical S3 object might look like this:

```
my-bucket/my-file.txt
```

The key (my-file.txt) is the name of the file, and the value is the contents of the file. The file might contain text, images, videos, or any other type of data.

## What is a Bucket?

A bucket is a container for objects. Every object in Amazon S3 must reside in a bucket. Buckets partition the namespace of objects stored in S3 at the top level. By creating a unique bucket name, you can guarantee that no other Amazon S3 user will be able to access your data.

Buckets can be used to host a static website. You can configure a bucket to serve web traffic directly from Amazon S3. This can be useful if you have a website with a large amount of static content (such as images, videos, or CSS and JavaScript files).

## How do I create a Bucket?

Creating a bucket is a simple, two-step process:

1.  Choose a name for your bucket.
2.  Create the bucket.

## How do I upload an Object to a Bucket?

After you create a bucket, you can upload objects to the bucket. To upload an object:

1.  Open the Amazon S3 console.
2.  Choose the bucket that you want to upload your object to.
3.  Choose Upload.
4.  Add the files that you want to upload.
5.  Choose Upload.

## How do I download an Object from a Bucket?

To download an object:

1.  Open the Amazon S3 console.
2.  Choose the bucket that you want to download your object from.
3.  Choose the object that you want to download.
4.  Choose Download.
5.  Choose Save.

## How do I delete an Object from a Bucket?

To delete an object:

1.  Open the Amazon S3 console.
2.  Choose the bucket that you want to delete your object from.
3.  Choose the object that you want to delete.
4.  Choose Delete.
5.  Choose Delete.

## How do I delete a Bucket?

To delete a bucket:

1.  Empty the bucket.
2.  Delete the bucket.

## What is an S3 Prefix?

An S3 prefix is a string that is used to identify a group of objects. S3 prefixes can be used to logically organize your Amazon S3 data. For example, you might use an S3 prefix to group all of the files that are related to a certain project.

S3 prefixes can be up to 1,024 characters long, and they must be unique within a bucket.

To create an S3 prefix:

1.  Open the Amazon S3 console.
2.  Choose the bucket that you want to create your prefix in.
3.  Choose Prefixes.
4.  Enter a prefix name.
5.  Choose Save.

## What is an S3 Policy?

An S3 policy is a document that specifies who has access to your S3 data and what actions they can perform on that data. S3 policies can be used to restrict access to specific buckets or objects.

Policies are attached to resources, such as buckets or objects. When a policy is attached to a resource, it defines the permissions for that resource.

## How do I create an S3 Policy?

To create an S3 policy, you need to create a policy document. A policy document is a JSON document that specifies the permissions for a resource.

## How do I attach an S3 Policy to a Bucket?

To attach an S3 policy to a bucket:

1.  Open the Amazon S3 console.
2.  Choose the bucket that you want to attach your policy to.
3.  Choose Permissions.
4.  Choose Add bucket policy.
5.  Enter your policy document.
6.  Choose Save.

## How do I attach an S3 Policy to an Object?

To attach an S3 policy to an object:

1.  Open the Amazon S3 console.
2.  Choose the bucket that contains the object that you want to attach your policy to.
3.  Choose the object.
4.  Choose Permissions.
5.  Choose Add object policy.
6.  Enter your policy document.
7.  Choose Save.

## How do I generate an S3 Policy?

The easiest way to generate an S3 policy is to use the Policy Generator. The Policy Generator is a tool that helps you create policies that are tailored to your specific needs.

To use the Policy Generator:

1.  Go to the Policy Generator website.
2.  Enter the ARN for the resource that you want to create a policy for.
3.  Select the permissions that you want to grant.
4.  Choose Generate Policy.
5.  Copy the policy document.

## What languages can I use to write S3 Policies?

S3 policies can be written in any of the following languages:

-   Java
-   JavaScript
-   Python
-   Ruby

## How do I find the ARN for my S3 Bucket?

To find the ARN for your S3 bucket:

1.  Open the Amazon S3 console.
2.  Choose the bucket that you want to find the ARN for.
3.  Choose Properties.
4.  Choose ARN.

## How do I find the ARN for my S3 Object?

To find the ARN for your S3 object:

1.  Open the Amazon S3 console.
2.  Choose the bucket that contains the object that you want to find the ARN for.
3.  Choose the object.
4.  Choose Properties.
5.  Choose ARN.

## Resources

-   [Amazon S3](https://aws.amazon.com/s3/)
-   [Getting Started with Amazon S3](https://docs.aws.amazon.com/AmazonS3/latest/gsg/GettingStartedWithS3.html)
-   [S3 Policy Generator](https://awspolicygen.s3.amazonaws.com/policygen.html)
-   [S3 Bucket Policy Examples](https://aws.amazon.com/articles/1834)
-   [S3 Object Policy Examples](https://aws.amazon.com/articles/1434)