---
title: AWS SageMaker: Building and Deploying Machine Learning Models in the Cloud
description: 
published: true
date: 2023-02-03T12:17:49.968Z
tags: 
editor: markdown
dateCreated: 2023-02-03T12:17:44.973Z
---

- [AWS SageMaker: creación e implementación de modelos de aprendizaje automático en la nube***Spanish** document is available*](/es/Knowledge-base/Cloud/aws-sagemaker-building-and-deploying-machine-learning-models-in-the-cloud)
{.links-list}
- [AWS SageMaker：在云中构建和部署机器学习模型***Chinese Simplified** document is available*](/zh/Knowledge-base/Cloud/aws-sagemaker-building-and-deploying-machine-learning-models-in-the-cloud)
{.links-list}
- [AWS SageMaker: 클라우드에서 기계 학습 모델 구축 및 배포***Korean** document is available*](/ko/Knowledge-base/Cloud/aws-sagemaker-building-and-deploying-machine-learning-models-in-the-cloud)
{.links-list}


# AWS SageMaker: Building and Deploying Machine Learning Models in the Cloud

Machine learning is a rapidly growing field of computer science that enables computers to learn from data without being explicitly programmed. Machine learning is already being used in a variety of applications, such as recommendation systems, image recognition, and fraud detection.

AWS SageMaker is a fully-managed service that provides developers and data scientists with the ability to build, train, and deploy machine learning models in the cloud. SageMaker removes the heavy lifting from each step of the machine learning process, making it easier to develop high-quality models.

## Getting Started with SageMaker

To get started with SageMaker, you first need to create an AWS account and sign up for SageMaker. Once you have an account, you can create an Amazon Elastic Compute Cloud (Amazon EC2) instance to use as your development environment. SageMaker provides a variety of pre-configured Amazon Machine Images (AMIs) that you can use to launch your EC2 instance.

Once you have launched your EC2 instance, you can connect to it using SSH and install the SageMaker Python SDK. The SDK provides a number of convenience functions that make working with SageMaker easier.

## Creating a SageMaker Model

There are two ways to create a SageMaker model:

- Use the SageMaker Python SDK to define a model using a Python script.
- Use the SageMaker web interface to create a model using a pre-trained machine learning algorithm.

### Creating a Model with the SageMaker Python SDK

To create a SageMaker model using the Python SDK, you first need to write a Python script that defines the model. The script should import the SageMaker Python SDK and define a subclass of the SageMaker.Model class.

Your model class must implement two methods:

- ```train()```, which is called when the model is training. This is where you should implement your training algorithm.
- ```predict()```, which is called when the model is deployed and is used to make predictions. This is where you should implement your prediction algorithm.

Once you have defined your model class, you can instantiate it and call the ```fit()``` method to train the model. The ```fit()``` method takes as input a SageMaker.TrainingInstance and a SageMaker.S3DataSource. The TrainingInstance is used to configure the training job, and the S3DataSource is used to specify the location of the training data.

After the training job is complete, you can call the ```deploy()``` method to deploy the trained model. The ```deploy()``` method takes as input a SageMaker.PredictorInstance and a SageMaker.S3DataSource. The PredictorInstance is used to configure the prediction endpoint, and the S3DataSource is used to specify the location of the model artifacts.

### Creating a Model with the SageMaker Web Interface

To create a SageMaker model using the web interface, you first need to launch a SageMaker notebook instance. A notebook instance is an Amazon EC2 instance that comes with the SageMaker Python SDK and Jupyter installed.

Once your notebook instance is up and running, you can open the Jupyter notebook and create a new SageMaker model. To do so, click on the "SageMaker Models" link in the left-hand navigation bar and then click on the "Create Model" button.

On the "Create Model" page, you will need to specify a name for your model and select a machine learning algorithm. SageMaker provides a number of pre-trained machine learning algorithms that you can use. For this example, we will use the XGBoost algorithm.

Next, you will need to specify the location of the training data. SageMaker can use data stored in Amazon S3, so you will need to create an Amazon S3 bucket and upload your training data to that bucket.

Once you have specified the location of the training data, you can click on the "Create Model" button to create the model.

## Training a SageMaker Model

Once you have created a SageMaker model, you can train it using the ```fit()``` method. The ```fit()``` method takes as input a SageMaker.TrainingInstance and a SageMaker.S3DataSource. The TrainingInstance is used to configure the training job, and the S3DataSource is used to specify the location of the training data.

 training job is complete, you can call the ```deploy()``` method to deploy the trained model. The ```deploy()``` method takes as input a SageMaker.PredictorInstance and a SageMaker.S3DataSource. The PredictorInstance is used to configure the prediction endpoint, and the S3DataSource is used to specify the location of the model artifacts.

## Conclusion

In this article, we have seen how to use AWS SageMaker to build and deploy machine learning models in the cloud. SageMaker makes it easy to train and deploy machine learning models by providing a fully-managed service that takes care of the heavy lifting for you.