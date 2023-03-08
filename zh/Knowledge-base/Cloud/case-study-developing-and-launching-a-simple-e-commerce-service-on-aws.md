---
title: 案例研究：在 AWS 上开发和启动简单的电子商务服务
description: 
published: true
date: 2023-02-04T11:18:08.674Z
tags: 
editor: markdown
dateCreated: 2023-02-04T11:18:07.006Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Case Study: Developing and Launching a Simple e-Commerce Service on AWS***English** document is available*](/en/Knowledge-base/Cloud/case-study-developing-and-launching-a-simple-e-commerce-service-on-aws)
{.links-list}


# 案例研究：在 AWS 上开发和启动简单的电子商务服务

在本案例研究中，我们将向您展示如何在 AWS 上开发和启动简单的电子商务服务。我们将介绍服务的架构和使用的不同 AWS 服务。我们还将提供一些代码示例来帮助您入门。

## 架构

我们将要开发的电子商务服务是一种简单的服务，由 Web 前端和后端数据库组成。 Web前端将使用PHP编程语言开发，后端数据库为MySQL。

![电商服务架构](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/architecture.png)

Web 前端将托管在 Amazon EC2 实例上，并将通过 Amazon CloudFront 分发进行访问。 CloudFront 是一个内容分发网络 (CDN)，它将缓存网站的静态内容（例如图像、CSS 和 JavaScript 文件）并以低延迟将其分发给用户。

后端数据库将托管在 Amazon RDS 上，用于存储产品和订单数据。 RDS 是一种托管关系数据库服务，可以轻松地在云中设置、操作和扩展关系数据库。

## 使用的 AWS 服务

本案例研究将使用以下 AWS 服务：

- 亚马逊 EC2
- 亚马逊云端
- 亚马逊 RDS
- 亚马逊 S3

## 设置后端数据库

我们将从设置后端数据库开始。我们将使用 Amazon RDS for MySQL。

首先，我们将创建一个新的 RDS 实例。我们将选择 MySQL 引擎和 db.t2.micro 实例类。

![创建新的 RDS 实例](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-01.png)

接下来，我们将为实例配置设置。我们将为实例命名，选择 MySQL 5.6.x 数据库引擎，然后选择 db.t2.micro 实例类。

![配置RDS实例](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-02.png)

接下来，我们将创建一个新数据库。我们将为数据库命名并选择 MySQL 5.6.x 数据库引擎。

![创建新数据库](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-03.png)

现在已经创建了数据库，我们需要创建一个用户并授予该用户访问数据库的权限。我们将使用用户名“ecommerce”和密码“password”创建一个用户。

![创建新用户](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-04.png)

接下来，我们将授予用户访问数据库的权限。我们将选择“电子商务”数据库和“电子商务”用户，然后单击“添加”按钮。

![授予对数据库的访问权限](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-05.png)

## 设置 Web 前端

现在后端数据库已经设置好，我们需要设置 Web 前端。为此，我们将使用 Amazon EC2。

首先，我们将创建一个新的 EC2 实例。我们将选择 Amazon Linux AMI 和 t2.micro 实例类型。

![创建一个新的 EC2 实例](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/ec2-01.png)

接下来，我们将为实例配置设置。我们将为实例命名，选择 Amazon Linux AMI，然后选择 t2.micro 实例类型。

![配置 EC2 实例](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/ec2-02.png)

现在已经创建了实例，我们需要通过 SSH 连接到实例。我们将使用在创建实例时下载的私钥。

![SSH 进入 EC2 实例](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/ec2-03.png)

登录实例后，我们需要安装 Apache Web 服务器、PHP 和 MySQL 客户端。我们将使用 yum 包管理器执行此操作。

```bash
$ sudo yum install -y httpd24 php70 mysql56-client
```

接下来，我们将启动 Apache Web 服务器。

```bash
$ sudo service httpd start
```

现在 Web 服务器已启动并正在运行，我们需要创建一个新的 PHP 文件。我们将此文件称为“index.php”，并将其放在“/var/www/html”目录中。

```php
<?php
  echo "Hello, world!";
?>
```

现在，我们需要编辑“/etc/httpd/conf/httpd.conf”文件并取消注释以下行：

```apache
LoadModule rewrite_module modules/mod_rewrite.so
```

接下来，我们将重新启动 Apache Web 服务器。

```bash
$ sudo service httpd restart
```

现在，我们需要创建一个新的 MySQL 用户。我们将使用之前创建的“电子商务”用户。我们将授予用户访问“电子商务”数据库的权限。

```sql
GRANT ALL ON ecommerce.* TO 'ecommerce'@'localhost' IDENTIFIED BY 'password';
```

现在已经创建了用户，我们需要将数据导入数据库。我们将使用 GitHub 存储库中包含的“products.sql”文件。

```bash
$ mysql -u ecommerce -p ecommerce < products.sql
```

## 测试应用程序

现在应用程序已设置，我们需要对其进行测试以确保一切都按预期工作。我们将从通过 Web 浏览器访问应用程序开始。

![测试应用程序](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/testing-01.png)

如我们所见，应用程序按预期工作。我们可以看到产品列表，我们可以将商品添加到购物车。

![测试应用程序](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/testing-02.png)

## 启动应用程序

现在应用程序已启动并正在运行，我们需要启动它。我们将通过创建 Amazon CloudFront 分配来完成此操作。

首先，我们将创建一个新的 CloudFront 分配。我们将选择“Web”传送方法和“Get”HTTP 方法。

![创建新的 CloudFront 分配](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-01.png)

接下来，我们将配置分发设置。我们将为分发命名，选择“Web”交付方法，然后选择“Get”HTTP 方法。

![配置 CloudFront 分布](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-02.png)

现在，我们需要创建一个新的原点。我们将选择“Custom Origin”类型并输入 EC2 实例的 URL。

![创建新源](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-03.png)

接下来，我们将配置源的设置。我们将为来源命名，选择“自定义来源”类型，然后输入我们的 EC2 实例的 URL。

![配置来源](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-04.png)

现在，我们需要创建一个新的默认缓存行为。我们将选择“默认 (*)”路径模式并为 Forward Headers 选择“Allow All”选项。

![创建新的默认缓存行为](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-05.png)

接下来，我们将配置默认缓存行为的设置。我们将选择“默认 (*)”路径模式并为 Forward Headers 选择“Allow All”选项。

![配置默认缓存行为](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-06.png)

现在，我们需要创建一个新的错误页面。我们将选择“404”错误代码并输入错误页面的 URL。

![创建一个新的错误页面](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-07.png)

接下来，我们将配置错误页面的设置。我们将选择“404”错误代码并输入错误页面的 URL。

![配置错误页面](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-08.png)

现在，我们需要创建一个新的 SSL 证书。我们将选择“自定义证书”选项并输入我们网站的域名。

![创建新的 SSL 证书](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-09.png)

接下来，我们将配置 SSL 证书的设置。我们将选择“自定义证书”选项并输入我们网站的域名。

![配置SSL证书](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-10.png)

现在，我们需要创建一个新的发行版。我们将选择“Web”传送方法和“Get”HTTP 方法。

![创建新发行版](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-11.png)

接下来，我们将配置分发设置。我们将为分发命名，选择“Web”交付方法，然后选择“Get”HTTP 方法。

![配置分发](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-12.png)

现在，我们需要创建一个新的默认缓存行为。我们将选择“默认 (*)”路径模式并为 Forward Headers 选择“Allow All”选项。

![创建新的默认缓存行为](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-13.png)

接下来，我们将配置默认缓存行为的设置。我们将选择“默认 (*)”路径模式并为 Forward Headers 选择“Allow All”选项。

![配置默认缓存行为](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-14.png)

现在，我们需要创建一个新的错误页面。我们将选择“404”错误代码并输入错误页面的 URL。

![创建一个新的错误页面](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-15.png)

接下来，我们将配置错误页面的设置。我们将选择“404”错误代码并输入错误页面的 URL。

![配置错误页面](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-16.png)

## 结论

在本案例研究中，我们向您展示了如何在 AWS 上开发和启动简单的电子商务服务。我们已经了解了该服务的架构以及所使用的不同 AWS 服务。我们还提供了一些代码示例来帮助您入门。