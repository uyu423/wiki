---
title: AWS Rekognition: Analyzing Image and Video Data with Computer Vision
description: 
published: true
date: 2023-02-05T17:55:25.765Z
tags: 
editor: markdown
dateCreated: 2023-02-05T17:55:20.300Z
---

- [AWS Rekognition: análisis de datos de imágenes y videos con visión artificial***Spanish** document is available*](/es/Knowledge-base/Cloud/aws-rekognition-analyzing-image-and-video-data-with-computer-vision)
{.links-list}
- [AWS Rekognition：使用计算机视觉分析图像和视频数据***Chinese Simplified** document is available*](/zh/Knowledge-base/Cloud/aws-rekognition-analyzing-image-and-video-data-with-computer-vision)
{.links-list}
- [AWS Rekognition: Computer Vision으로 이미지 및 비디오 데이터 분석***Korean** document is available*](/ko/Knowledge-base/Cloud/aws-rekognition-analyzing-image-and-video-data-with-computer-vision)
{.links-list}


# AWS Rekognition: Analyzing Image and Video Data with Computer Vision

AWS Rekognition is a cloud-based service that makes it easy to add powerful visual analysis to your applications. With Rekognition, you can detect objects, scenes, and faces in images and videos, as well as identify inappropriate content. Rekognition also provides highly accurate facial recognition and facial analysis, such as detecting emotions, gender, and age range. You can use these features to create smarter applications that can automatically moderate content, personalize experiences for your customers, and improve security. 

Rekognition uses deep learning algorithms to provide these capabilities. Deep learning is a type of machine learning that teaches computers to learn from data, without being explicitly programmed.Deep learning is part of a broader family of machine learning methods based on learning data representations, as opposed to task-specific algorithms. 

## Why Use Rekognition?

Rekognition makes it easy to add powerful visual analysis to your applications. With Rekognition, you can detect objects, faces, and scenes in images and videos, as well as identify inappropriate content. Rekognition also provides highly accurate facial recognition and facial analysis. You can use these features to create smarter applications that can automatically moderate content, personalize experiences for your customers, and improve security. 

## Getting Started with Rekognition

To get started with Rekognition, you first need to create an AWS account and sign up for the service. You can then create a Rekognition project in the AWS Management Console. A Rekognition project is a logical container for all the resources that you need to use Rekognition. After you create a project, you can add images and videos to analyze, and configure Amazon Simple Storage Service (Amazon S3) buckets to store the results of your analysis. 

## Analyzing Images and Videos

Rekognition makes it easy to analyze images and videos for a wide variety of use cases, such as identifying objects, faces, and scenes; detecting inappropriate content; and recognizing celebrities and landmarks. 

Rekognition provides two main ways to analyze images and videos:

* **DetectLabels** returns a list of labels (such as "Dog" or "Cat") that are detected in an image. Each label also includes a confidence score that indicates how confident Rekognition is that the label has been correctly identified. 

* **DetectModerationLabels** returns a list of labels that identify unsafe or inappropriate content in an image. For example, a label such as "Lascivious" or "Violence" indicates that the image contains adult content. Each label also includes a confidence score that indicates how confident Rekognition is that the label has been correctly identified. 

You can also use the **AnalyzeFaces** operation to analyze faces in an image and get information about the faces, such as the emotions that are detected, the estimated age of the face, whether the face is wearing sunglasses, and more. 

## Recognizing Celebrities and Landmarks

Rekognition can recognize celebrities and landmarks in images. For example, you can use the **RecognizeCelebrities** operation to identify celebrities in an image. You can also use the **DetectLabels** operation to identify landmarks in an image. 

## Implementing Rekognition

Rekognition is a web service that you can call using the AWS SDKs. You can call Rekognition using the AWS Management Console, the AWS Command Line Interface, or programmatically using one of the AWS SDKs. 

## Pricing

Rekognition charges you for the number of images and videos that you analyze and the face metadata that you store. Rekognition does not charge you for the number of images and videos that you store. 

## Resources

* [AWS Rekognition](https://aws.amazon.com/rekognition/)
* [DetectLabels](https://docs.aws.amazon.com/rekognition/latest/dg/API_DetectLabels.html)
* [DetectModerationLabels](https://docs.aws.amazon.com/rekognition/latest/dg/API_DetectModerationLabels.html)
* [AnalyzeFaces](https://docs.aws.amazon.com/rekognition/latest/dg/API_AnalyzeFaces.html)
* [RecognizeCelebrities](https://docs.aws.amazon.com/rekognition/latest/dg/API_RecognizeCelebrities.html)
* [AWS SDKs](https://aws.amazon.com/tools/)
* [Pricing](https://aws.amazon.com/rekognition/pricing/)