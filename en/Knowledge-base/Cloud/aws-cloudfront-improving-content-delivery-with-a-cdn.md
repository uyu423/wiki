---
title: AWS CloudFront: Improving Content Delivery with a CDN
description: 
published: true
date: 2023-02-01T14:17:44.997Z
tags: 
editor: markdown
dateCreated: 2023-02-01T14:17:41.534Z
---

- [AWS CloudFront: CDN으로 콘텐츠 전송 개선***Korean** version of this document is available*](/ko/Knowledge-base/Cloud/aws-cloudfront-improving-content-delivery-with-a-cdn)
{.links-list}
- [AWS CloudFront：使用 CDN 改进内容交付***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Cloud/aws-cloudfront-improving-content-delivery-with-a-cdn)
{.links-list}


  Include an opening and closing sentence for the article.

# AWS CloudFront: Improving Content Delivery with a CDN

If you're looking to improve the performance of your website or web application, one of the first places to look is your content delivery network (CDN). A CDN can help to improve the loading speed of your content by caching it at locations around the world, so that users can access it more quickly.

One of the most popular CDNs is Amazon CloudFront, which is a service that sits on top of Amazon's AWS infrastructure. CloudFront is a global CDN that delivers your content through a network of edge locations. It's easy to set up and configure, and it integrates with other AWS services.

In this article, we'll take a look at how to improve content delivery with CloudFront. We'll cover the following topics:

- Setting up CloudFront
- Configuring CloudFront
- Using CloudFront with other AWS services

## Setting up CloudFront

To get started with CloudFront, you'll need to create a distribution. A distribution is a collection of AWS resources that are used to deliver your content. To create a distribution, you'll need to specify the following:

- The origin of your content. This can be an Amazon S3 bucket, an Amazon Elastic Compute Cloud (EC2) instance, or an HTTP server.
- The distribution's configuration. This includes the distribution's cache behavior and other settings.
- The distribution's price class. This determines the pricing for the distribution, based on the region where the user is accessing the content from.

Once you've created a distribution, you'll need to wait for it to be deployed. This can take up to 15 minutes. Once the distribution is deployed, you'll be able to access your content through the CloudFront URL.

## Configuring CloudFront

Once you've set up your CloudFront distribution, you'll need to configure it to work with your website or web application. The first thing you'll need to do is create a cache behavior. A cache behavior determines how CloudFront handles requests for your content.

There are two types of cache behaviors: default and custom. Default cache behaviors are applied to all of the files in your distribution, unless you specify a custom cache behavior for a specific file or folder. Custom cache behaviors are applied to specific files or folders, and take precedence over the default cache behavior.

To create a cache behavior, you'll need to specify the following:

- The path pattern that the cache behavior applies to. This can be a specific file or folder, or a wildcard pattern.
- The origin that the cache behavior applies to. This is the origin that CloudFront will fetch the content from.
- The default TTL (time to live) for the cache behavior. This is the amount of time that CloudFront will cache the content.
- The maximum TTL for the cache behavior. This is the maximum amount of time that CloudFront will cache the content.
- The minimum TTL for the cache behavior. This is the minimum amount of time that CloudFront will cache the content.

Once you've created a cache behavior, you can specify additional settings, such as the following:

- The allowed HTTP methods. This determines which HTTP methods CloudFront will allow for the cache behavior.
- The cached HTTP methods. This determines which HTTP methods CloudFront will cache for the cache behavior.
- The forwarded headers. This determines which headers CloudFront will forward to the origin for the cache behavior.

## Using CloudFront with other AWS services

CloudFront can be used with other AWS services to improve the performance of your website or web application. For example, you can use CloudFront with Amazon S3 to deliver content from an S3 bucket.

To do this, you'll need to create a bucket and then configure CloudFront to use the bucket as an origin. You can do this by creating a cache behavior for the bucket.

Once you've done this, you can use CloudFront to deliver the content from the bucket to users. CloudFront will cache the content at edge locations around the world, so that users can access it more quickly.

You can also use CloudFront with Amazon EC2 to deliver content from an EC2 instance. To do this, you'll need to create an instance and then configure CloudFront to use the instance as an origin. You can do this by creating a cache behavior for the instance.

Once you've done this, you can use CloudFront to deliver the content from the instance to users. CloudFront will cache the content at edge locations around the world, so that users can access it more quickly.

## Conclusion

In this article, we've looked at how to improve content delivery with CloudFront. We've covered the following topics:

- Setting up CloudFront
- Configuring CloudFront
- Using CloudFront with other AWS services

If you're looking to improve the performance of your website or web application, CloudFront is a great option. It's easy to set up and configure, and it integrates with other AWS services.