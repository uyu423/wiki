---
title: AWS Rekognition：使用计算机视觉分析图像和视频数据
description: 
published: true
date: 2023-02-05T17:55:21.865Z
tags: 
editor: markdown
dateCreated: 2023-02-05T17:55:20.298Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [AWS Rekognition: Analyzing Image and Video Data with Computer Vision***English** document is available*](/en/Knowledge-base/Cloud/aws-rekognition-analyzing-image-and-video-data-with-computer-vision)
{.links-list}


# AWS Rekognition：使用计算机视觉分析图像和视频数据

AWS Rekognition 是一种基于云的服务，可以轻松地为您的应用程序添加强大的可视化分析。借助 Rekognition，您可以检测图像和视频中的对象、场景和人脸，以及识别不当内容。 Rekognition 还提供高度准确的面部识别和面部分析，例如检测情绪、性别和年龄范围。您可以使用这些功能创建更智能的应用程序，这些应用程序可以自动调节内容、为您的客户提供个性化体验并提高安全性。

Rekognition 使用深度学习算法来提供这些功能。深度学习是一种机器学习，它教会计算机从数据中学习，而无需明确编程。深度学习是更广泛的机器学习方法家族的一部分，它基于学习数据表示，而不是特定于任务的算法。

## 为什么要使用 Rekognition？

Rekognition 可以轻松地向您的应用程序添加强大的可视化分析。借助 Rekognition，您可以检测图像和视频中的对象、面部和场景，以及识别不当内容。 Rekognition 还提供高度准确的面部识别和面部分析。您可以使用这些功能创建更智能的应用程序，这些应用程序可以自动调节内容、为您的客户提供个性化体验并提高安全性。

## Rekognition 入门

要开始使用 Rekognition，您首先需要创建一个 AWS 账户并注册该服务。然后，您可以在 AWS 管理控制台中创建一个 Rekognition 项目。 Rekognition 项目是您使用 Rekognition 所需的所有资源的逻辑容器。创建项目后，您可以添加图像和视频进行分析，并配置 Amazon Simple Storage Service (Amazon S3) 存储桶来存储分析结果。

## 分析图像和视频

Rekognition 可以轻松分析各种用例的图像和视频，例如识别对象、人脸和场景；检测不当内容；并识别名人和地标。

Rekognition 提供了两种主要的图像和视频分析方法：

* **DetectLabels** 返回在图像中检测到的标签列表（例如“狗”或“猫”）。每个标签还包括一个置信度分数，表明 Rekognition 对标签已被正确识别的信心。

* **DetectModerationLabels** 返回标识图像中不安全或不当内容的标签列表。例如，“淫荡”或“暴力”等标签表示图片包含成人内容。每个标签还包括一个置信度分数，表明 Rekognition 对标签已被正确识别的信心。

您还可以使用 **AnalyzeFaces** 操作来分析图像中的人脸并获取有关人脸的信息，例如检测到的情绪、人脸的估计年龄、人脸是否戴墨镜等。

## 识别名人和地标

Rekognition 可以识别图像中的名人和地标。例如，您可以使用 **RecognizeCelebrities** 操作来识别图像中的名人。您还可以使用 **DetectLabels** 操作来识别图像中的地标。

## 实现重新识别

Rekognition 是一种 Web 服务，您可以使用 AWS 开发工具包调用它。您可以使用 AWS 管理控制台、AWS 命令行界面或以编程方式使用其中一个 AWS 开发工具包调用 Rekognition。

## 价钱

Rekognition 会根据您分析的图像和视频的数量以及您存储的人脸元数据向您收费。 Rekognition 不会就您存储的图像和视频的数量向您收费。

## 资源

* [AWS 识别](https://aws.amazon.com/rekognition/)
* [检测标签](https://docs.aws.amazon.com/rekognition/latest/dg/API_DetectLabels.html)
* [DetectModerationLabels](https://docs.aws.amazon.com/rekognition/latest/dg/API_DetectModerationLabels.html)
* [AnalyzeFaces](https://docs.aws.amazon.com/rekognition/latest/dg/API_AnalyzeFaces.html)
* [识别名人](https://docs.aws.amazon.com/rekognition/latest/dg/API_RecognizeCelebrities.html)
* [AWS SDK](https://aws.amazon.com/tools/)
* [定价](https://aws.amazon.com/rekognition/pricing/)