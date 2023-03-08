---
title: Continuous Integration and Continuous Deployment on AWS and Azure
description: 
published: true
date: 2023-02-04T16:55:51.598Z
tags: 
editor: markdown
dateCreated: 2023-02-04T16:55:49.813Z
---

- [Integración continua e implementación continua en AWS y Azure***Spanish** document is available*](/es/Knowledge-base/Cloud/continuous-integration-and-continuous-deployment-on-aws-and-azure)
{.links-list}
- [AWS 和 Azure 上的持续集成和持续部署***Chinese Simplified** document is available*](/zh/Knowledge-base/Cloud/continuous-integration-and-continuous-deployment-on-aws-and-azure)
{.links-list}
- [AWS 및 Azure에서 지속적 통합 및 지속적 배포***Korean** document is available*](/ko/Knowledge-base/Cloud/continuous-integration-and-continuous-deployment-on-aws-and-azure)
{.links-list}


# Continuous Integration and Continuous Deployment on AWS and Azure

Cloud platforms such as AWS and Azure offer many benefits for developers, including the ability to quickly scale resources and the flexibility to use a variety of programming languages and tools. These platforms also make it easy to set up continuous integration (CI) and continuous deployment (CD) pipelines.

In this article, we will take a look at how to set up CI/CD pipelines on AWS and Azure. We will also discuss some of the benefits and challenges of using these platforms for CI/CD.

## What is Continuous Integration?

Continuous integration (CI) is the practice of automatically building and testing code changes as they are made. This allows developers to detect and fix errors quickly, and it helps ensure that the code base is always in a deployable state.

 CI pipelines are typically triggered by code commits, and they typically include the following steps:

- Code is built and tested automatically.
- Automated tests are run to check for errors.
- If the tests pass, the code is deployed to a staging environment.
- If the tests fail, the code is not deployed and the developers are notified.

## What is Continuous Deployment?

Continuous deployment (CD) is the practice of automatically deploying code changes to a production environment. This allows developers to get new features and fixes to users as quickly as possible.

CD pipelines typically include the following steps:

- Code is built and tested automatically.
- If the tests pass, the code is deployed to a production environment.
- If the tests fail, the code is not deployed and the developers are notified.

## Setting up a CI/CD Pipeline on AWS

AWS offers a number of services that can be used to set up CI/CD pipelines. In this section, we will take a look at how to set up a simple CI/CD pipeline using AWS CodePipeline and AWS CodeBuild.

### Prerequisites

Before you begin, you will need the following:

- An AWS account
- A GitHub account
- A code repository in GitHub

### Setting up AWS CodePipeline

AWS CodePipeline is a service that can be used to automate the process of building, testing, and deploying code changes.

To set up a CI pipeline using CodePipeline, you will need to create a new CodePipeline pipeline. To do this, log into the AWS console and navigate to the CodePipeline service.

Click the "Create Pipeline" button to begin.

On the "Select Pipeline Settings" page, give your pipeline a name and choose a region. Then, click the "Next" button.

On the "Add Source" page, select "GitHub" as the source provider. Then, choose the repository and branch that you want to use for your pipeline. Finally, click the "Next" button.

On the "Add Build Stage" page, select "AWS CodeBuild" as the build provider. Then, choose a name for your build stage and click the "Next" button.

On the "Configure Build Stage" page, select the "Linux, Ubuntu" operating system and the "Standard" runtime. Then, choose the "aws/codebuild/standard:4.0" image.

In the "EnvironmentVariables" section, add the following environment variables:

- "Name": "REPOSITORY_NAME"
- "Value": "Your GitHub repository name"

In the "BuildSpec" section, enter the following build commands:

- "version: 0.2"
- "phases:"
- "pre_build:"
- "commands:"
- "echo Logging in to GitHub..."
- "${{git-credential}} fill"
- "build:"
- "commands:"
- "echo Build started on `date`"
- "echo Building site..."
- "hugo"
- "post_build:"
- "commands:"
- "echo Build completed on `date`"

Click the "Save Build Project" button to save your build project.

On the "Add Deploy Stage" page, select "AWS CodeDeploy" as the deploy provider. Then, choose a name for your deploy stage and click the "Next" button.

On the "Configure Deploy Stage" page, select the "EC2/on-premises" instance type and the "Default" deployment type. Then, enter the following deployment configuration:

- "Application Name": "Your GitHub repository name"
- "Deployment Group Name": "Your GitHub repository name-deploy"
- "Service Role ARN": "arn:aws:iam::aws:policy/service-role/AWSCodeDeployRole"

Click the "Save Deployment Group" button to save your deployment group.

On the "Review" page, review your pipeline settings and then click the "Create Pipeline" button.

Your CI pipeline is now ready to use. Whenever you commit code changes to your GitHub repository, CodePipeline will automatically build and deploy your code.

## Setting up a CI/CD Pipeline on Azure

Azure offers a number of services that can be used to set up CI/CD pipelines. In this section, we will take a look at how to set up a simple CI/CD pipeline using Azure DevOps and Azure Pipelines.

### Prerequisites

Before you begin, you will need the following:

- An Azure account
- A GitHub account
- A code repository in GitHub

### Setting up Azure DevOps

Azure DevOps is a service that can be used to automate the process of building, testing, and deploying code changes.

To set up a CI pipeline using Azure DevOps, you will need to create a new Azure DevOps project. To do this, log into the Azure portal and navigate to the Azure DevOps service.

Click the "New Project" button to begin.

Give your project a name and then click the "Create" button.

Your Azure DevOps project is now ready to use.

### Setting up Azure Pipelines

Azure Pipelines is a service that can be used to automate the process of building, testing, and deploying code changes.

To set up a CI pipeline using Azure Pipelines, you will need to create a new Azure Pipeline. To do this, log into the Azure portal and navigate to the Azure Pipelines service.

Click the "New Pipeline" button to begin.

On the "Select a Source" page, select "GitHub" as the source provider. Then, choose the repository and branch that you want to use for your pipeline. Finally, click the "Continue" button.

On the "Select a Template" page, select the "Starter pipeline" template and click the "Continue" button.

On the "Configure your pipeline" page, enter the following YAML code:

- trigger:
- branches:
- include:
- master
- path: /
- readme.md
- stages:
- - stage: Build
- jobs:
- - job: Build
- steps:
- - checkout: self
- - task: UseDotNet@2
- inputs:
- packageType: sdk
- version: 3.1.100
- - task: DotNetCoreCLI@2
- inputs:
- command: build
- arguments: --configuration Release
- - stage: Test
- jobs:
- - job: Test
- steps:
- - checkout: self
- - task: DotNetCoreCLI@2
- inputs:
- command: test
- arguments: --no-build --configuration Release
- - stage: Deploy
- jobs:
- - job: Deploy
- steps:
- - checkout: self
- - task: CopyFiles@2
- inputs:
- SourceFolder: '$(Pipeline.Workspace)'
- Contents: '**/*'
- TargetFolder: '$(Build.ArtifactStagingDirectory)'
- - task: PublishBuildArtifacts@1
- inputs:
- PathtoPublish: '$(Build.ArtifactStagingDirectory)'
- ArtifactName: 'drop'
- publishLocation: 'Container'

Click the "Save and Run" button to save your pipeline and run it.

Your CI pipeline is now ready to use. Whenever you commit code changes to your GitHub repository, Azure Pipelines will automatically build and deploy your code.

## Conclusion

In this article, we have looked at how to set up CI/CD pipelines on AWS and Azure. We have also discussed some of the benefits and challenges of using these platforms for CI/CD.