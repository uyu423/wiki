---
title: AWS SageMaker：在云中构建和部署机器学习模型
description: 
published: true
date: 2023-02-03T12:17:46.579Z
tags: 
editor: markdown
dateCreated: 2023-02-03T12:17:44.965Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [AWS SageMaker: Building and Deploying Machine Learning Models in the Cloud***English** document is available*](/en/Knowledge-base/Cloud/aws-sagemaker-building-and-deploying-machine-learning-models-in-the-cloud)
{.links-list}


# AWS SageMaker：在云中构建和部署机器学习模型

机器学习是一个快速发展的计算机科学领域，它使计算机无需明确编程即可从数据中学习。机器学习已经被用于各种应用，例如推荐系统、图像识别和欺诈检测。

AWS SageMaker 是一项完全托管的服务，可为开发人员和数据科学家提供在云中构建、训练和部署机器学习模型的能力。 SageMaker 消除了机器学习过程中每一步的繁重工作，使开发高质量模型变得更加容易。

## 开始使用 SageMaker

要开始使用 SageMaker，您首先需要创建一个 AWS 账户并注册 SageMaker。拥有帐户后，您可以创建一个 Amazon Elastic Compute Cloud (Amazon EC2) 实例以用作您的开发环境。 SageMaker 提供各种预配置的 Amazon 系统映像 (AMI)，您可以使用它们来启动 EC2 实例。

启动 EC2 实例后，您可以使用 SSH 连接到它并安装 SageMaker Python SDK。该 SDK 提供了许多方便的功能，使使用 SageMaker 变得更加容易。

## 创建 SageMaker 模型

创建 SageMaker 模型有两种方法：

- 使用 SageMaker Python SDK 通过 Python 脚本定义模型。
- 使用 SageMaker Web 界面使用预训练的机器学习算法创建模型。

### 使用 SageMaker Python SDK 创建模型

要使用 Python SDK 创建 SageMaker 模型，您首先需要编写定义模型的 Python 脚本。该脚本应导入 SageMaker Python SDK 并定义 SageMaker.Model 类的子类。

您的模型类必须实现两个方法：

- ```train()```，在模型训练时调用。这是您应该实施训练算法的地方。
- ```predict()```，在部署模型时调用，用于进行预测。这是您应该实施预测算法的地方。

一旦你定义了你的模型类，你就可以实例化它并调用```fit()```方法来训练模型。 ```fit()``` 方法将 SageMaker.TrainingInstance 和 SageMaker.S3DataSource 作为输入。 TrainingInstance 用于配置训练作业，S3DataSource 用于指定训练数据的位置。

训练作业完成后，可以调用```deploy()```方法部署训练好的模型。 ```deploy()``` 方法将 SageMaker.PredictorInstance 和 SageMaker.S3DataSource 作为输入。 PredictorInstance 用于配置预测端点，S3DataSource 用于指定模型工件的位置。

### 使用 SageMaker Web 界面创建模型

要使用 Web 界面创建 SageMaker 模型，您首先需要启动 SageMaker 笔记本实例。笔记本实例是安装了 SageMaker Python SDK 和 Jupyter 的 Amazon EC2 实例。

一旦您的笔记本实例启动并运行，您就可以打开 Jupyter 笔记本并创建一个新的 SageMaker 模型。为此，请单击左侧导航栏中的“SageMaker 模型”链接，然后单击“创建模型”按钮。

在“创建模型”页面上，您需要为模型指定名称并选择机器学习算法。 SageMaker 提供了许多您可以使用的预训练机器学习算法。对于此示例，我们将使用 XGBoost 算法。

接下来，您需要指定训练数据的位置。 SageMaker 可以使用存储在 Amazon S3 中的数据，因此您需要创建一个 Amazon S3 存储桶并将您的训练数据上传到该存储桶。

指定训练数据的位置后，您可以单击“创建模型”按钮来创建模型。

## 训练 SageMaker 模型

创建 SageMaker 模型后，您可以使用 ```fit()``` 方法对其进行训练。 ```fit()``` 方法将 SageMaker.TrainingInstance 和 SageMaker.S3DataSource 作为输入。 TrainingInstance 用于配置训练作业，S3DataSource 用于指定训练数据的位置。

 训练工作完成，可以调用```deploy()```方法部署训练好的模型。 ```deploy()``` 方法将 SageMaker.PredictorInstance 和 SageMaker.S3DataSource 作为输入。 PredictorInstance 用于配置预测端点，S3DataSource 用于指定模型工件的位置。

## 结论

在本文中，我们了解了如何使用 AWS SageMaker 在云中构建和部署机器学习模型。 SageMaker 通过提供完全托管的服务来为您处理繁重的工作，从而使训练和部署机器学习模型变得容易。