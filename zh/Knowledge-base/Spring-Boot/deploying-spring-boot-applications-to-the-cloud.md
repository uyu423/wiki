---
title: 将 Spring Boot 应用程序部署到云端
description: 
published: true
date: 2023-02-17T18:03:19.335Z
tags: 
editor: markdown
dateCreated: 2023-01-30T11:02:21.831Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Deploying Spring Boot Applications to the Cloud***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/deploying-spring-boot-applications-to-the-cloud)
{.links-list}


# 将 Spring Boot 应用程序部署到云端

当涉及到部署应用程序的平台时，如今的开发人员有太多的选择余地。云已成为新应用程序部署的事实标准，三大提供商——亚马逊网络服务 (AWS)、微软 Azure 和谷歌云平台 (GCP)——都提供强大的服务。

在本文中，我们将专注于将 Spring Boot 应用程序部署到云中。 Spring Boot 是一种流行的基于 Java 的框架，可以轻松创建独立的、生产级的基于 Spring 的应用程序，您可以“直接运行”。

有多种方法可以将 Spring Boot 应用程序部署到云中。我们将介绍两种最流行的方法：

* 部署到平台即服务 (PaaS)
* 部署到基础架构即服务 (IaaS)

## 部署到平台即服务 (PaaS)

平台即服务 (PaaS) 是一种云计算模型，在该模型中，第三方提供商通常以平台即服务堆栈的形式通过 Internet 向用户提供平台和基础设施工具。

PaaS在云端提供了完整的开发和部署环境，让开发者可以专注于编写代码，而不用担心底层基础设施。

### 英雄库

一个流行的 PaaS 提供商是 [Heroku](https://www.heroku.com/)，它提供了一个为托管 Spring Boot 应用程序而优化的平台。

Heroku 的吸引力在于它的简单性。要将 Spring Boot 应用程序部署到 Heroku，您只需在项目的根目录中创建一个包含以下行的“Procfile”：

    网络：java -jar target/<您的应用程序名称>.jar

您还需要将以下依赖项添加到您的 pom.xml 文件中：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-tomcat</artifactId>
    <scope>provided</scope>
</dependency>
```

完成后，您可以使用 `heroku` 命令行工具将您的应用程序部署到 Heroku。首先，您需要创建一个新的 Heroku 应用程序：

    heroku 创建

然后，您可以将您的应用程序部署到 Heroku：

    git push heroku 大师

您的应用程序现在将在 `https://<your-app-name>.herokuapp.com` 启动并运行。

### 云铸造厂

[Cloud Foundry](https://www.cloudfoundry.org/) 是另一个流行的 PaaS 提供商，值得考虑用于部署 Spring Boot 应用程序。

与 Heroku 一样，Cloud Foundry 可以轻松部署 Spring Boot 应用程序。要将 Spring Boot 应用程序部署到 Cloud Foundry，您首先需要在项目的根目录中创建一个 manifest.yml 文件。此文件包含有关您的应用程序的信息，例如名称、内存限制和主机名。

这是一个示例 manifest.yml 文件：

```yaml
---
applications:
- name: my-app
  memory: 512M
  disk_quota: 1024M
  instances: 1
  path: build/libs/my-app.jar
  env:
    JAVA_OPTS: -Djava.security.egd=file:///dev/urandom
  buildpack: https://github.com/cloudfoundry/java-buildpack
```

然后，您可以使用 `cf` 命令行工具将您的应用程序部署到 Cloud Foundry：

    对比推

您的应用程序现在将在 `https://<your-app-name>.cfapps.io` 启动并运行。

## 部署到基础架构即服务 (IaaS)

基础架构即服务 (IaaS) 是一种云计算模型，在该模型中，第三方提供商通过 Internet 向用户提供基础架构（通常是服务器、存储和网络）。

IaaS 为开发人员提供了比 PaaS 更多的底层基础设施控制权，但也需要更多的设置和维护工作。

### AWS

Amazon Web Services (AWS) 是最受欢迎的 IaaS 提供商，提供范围广泛的可用于托管 Spring Boot 应用程序的服务。在本节中，我们将重点介绍如何使用 [Elastic Beanstalk](https://aws.amazon.com/elasticbeanstalk/) 将 Spring Boot 应用程序部署到 AWS。

Elastic Beanstalk 是一项服务，可让您在 Apache、Nginx、Passenger 和 IIS 等熟悉的服务器上轻松部署、管理和扩展使用 Java、.NET、PHP、Node.js、Python 和 Ruby 开发的 Web 应用程序和服务.

要将 Spring Boot 应用程序部署到 Elastic Beanstalk，您首先需要在项目的 src/main/resources 目录中创建一个 application.properties 文件。此文件包含有关您的应用程序的信息，例如名称、版本和环境。

这是一个示例 application.properties 文件：

```properties
name=my-app
version=1.0.0
environment=production
```

您还需要在项目的根目录中创建一个“AWS Elastic Beanstalk”文件。此文件包含有关应用程序环境的信息，例如区域、实例类型和安全组。

这是一个示例 AWS Elastic Beanstalk 文件：

```yaml
---
AWSEBDebuggingMode: true
AWSEBEnvironmentVariables:
  JAVA_OPTS: -Djava.security.egd=file:///dev/urandom
AWSEBServiceRole: null
AWSEBUseAmi64: true
AWSEluaticLoadBalancerScheme: internet-facing
AWSEBSecurityGroups:
- my-security-group
AWSEBSubnets:
- subnet-12345678
AWSEBIAMInstanceProfile: null
AWSEBRDSDatabaseInstance: null
AWSEBRDSDatabasePassword: null
AWSEBRDSDatabaseUsername: null
AWSEBRDSDatabaseEngine: null
AWSEBRDSDatabaseName: null
AWSEBRDSSnapshotIdentifier: null
AWSEBRDSAllocatedStorage: null
AWSEBRDSStorageType: null
AWSEBRDSMultiAZ: null
AWSEBRDSIops: null
AWSEBRDSEncrypted: null
AWSEBRDSKmsKeyId: null
AWSEBRDSDeletionPolicy: null
AWSEBS3Key: my-s3-key
AWSEBS3Bucket: my-s3-bucket
AWSEBS3ObjectKey: my-s3-object-key
AWSEBS3ETag: my-s3-etag
AWSEBS3VersionId: my-s3-version-id
AWSEBS3Region: us-east-1
AWSEBS3StorageClass: STANDARD
AWSEBNotificationEndpoint: null
AWSEBNotificationProtocol: null
AWSEBNotificationTopicARN: null
AWSEBManagedActionHistoryRetentionPeriod: 14
```

创建这些文件后，您可以使用 `eb` 命令行工具将您的应用程序部署到 Elastic Beanstalk。首先，您需要创建一个新的 Elastic Beanstalk 应用程序：

    电子创建

然后，您可以将应用程序部署到 Elastic Beanstalk：

    部署

您的应用程序现在将在“http://<your-app-name>.elasticbeanstalk.com”上启动并运行。

###蔚蓝

Microsoft Azure 是另一个流行的 IaaS 提供商，它提供了许多可用于托管 Spring Boot 应用程序的服务。在本节中，我们将重点介绍如何使用 [App Service](https://docs.microsoft.com/en-us/azure/app-service/overview) 将 Spring Boot 应用程序部署到 Azure。

App Service 是一项 Microsoft Azure PaaS 服务，针对托管 Web 应用程序和 Web 服务进行了优化。要将 Spring Boot 应用程序部署到 App Service，首先需要在项目的 src/main/resources 目录中创建一个 application.properties 文件。此文件包含有关您的应用程序的信息，例如名称、版本和环境。

这是一个示例 application.properties 文件：

```properties
name=my-app
version=1.0.0
environment=production
```

您还需要在项目的 src/main/webapp/WEB-INF 目录中创建一个 web.xml 文件。此文件包含有关应用程序的 servlet 的信息，例如 servlet 类和映射。

这是一个示例 web.xml 文件：

```xml
<web-app>
  <servlet>
    <servlet-name>my-app</servlet-name>
    <servlet-class>org.springframework.boot.web.servlet.support.SpringBootServletInitializer</servlet-class>
  </servlet>
  <servlet-mapping>
    <servlet-name>my-app</servlet-name>
    <url-pattern>/</url-pattern>
  </servlet-mapping>
</web-app>
```

创建这些文件后，您可以使用“az”命令行工具将应用程序部署到应用服务。首先，您需要创建一个新的 App Service 应用程序：

    az appservice plan create --name my-app-service-plan --resource-group 我的资源组 --sku S1

然后，您可以将应用程序部署到 App Service：

    az webapp create --resource-group my-resource-group --plan my-app-service-plan --name my-app --deployment-container-image="mcr.microsoft.com/java/jdk:8u192-祖鲁高山”

您的应用程序现在将在“http://my-app.azurewebsites.net”上启动并运行。

## 结论

在本文中，我们研究了将 Spring Boot 应用程序部署到云的两种不同方法：

* 部署到平台即服务 (PaaS)
* 部署到基础架构即服务 (IaaS)

每种方法都有自己的优点和缺点，因此为您的应用程序选择正确的方法很重要。

如果您正在寻找一种快速简便的方法来让您的应用程序在云中启动和运行，那么 PaaS 就是您的不二之选。 Heroku 和 Cloud Foundry 是值得考虑的两个流行的 PaaS 提供商。

如果您正在寻求对底层基础设施的更多控制，那么 IaaS 是您的不二之选。 AWS 和 Azure 是两个流行的 IaaS 提供商，它们提供范围广泛的服务，可用于托管 Spring Boot 应用程序。