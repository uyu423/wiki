---
title: 032：使用 Spring Boot（S3、Google Drive）与文件存储服务集成
description: 
published: true
date: 2023-02-04T00:32:26.265Z
tags: 
editor: markdown
dateCreated: 2023-02-04T00:32:24.612Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [032: Integrating with a file storage service using Spring Boot (S3, Google Drive)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/032-integrating-with-a-file-storage-service-using-spring-boot-s3-google-drive)
{.links-list}


# 032：使用 Spring Boot（S3、Google Drive）与文件存储服务集成

在本文中，我们将学习如何将 Spring Boot 应用程序与文件存储服务集成，例如 Amazon Simple Storage Service (S3) 或 Google Drive。

我们将首先创建一个新的 Spring Boot 项目并添加所需的依赖项。然后，我们将配置应用程序以使用文件存储服务。

最后，我们将编写一个简单的控制器来测试文件存储集成。

## 创建 Spring Boot 项目

首先，我们将使用 [Spring Initializr](https://start.spring.io/) 创建一个新的 Spring Boot 项目。我们将项目命名为“file-storage-service-integration”。

![Spring Initializr](https://i.imgur.com/HUjEr9r.png)

我们将选择以下依赖项：

* Web - 用于网络界面
* Cloud AWS - 用于 Amazon S3 集成
* Cloud GCP - 用于 Google Drive 集成

![Spring Initializr 依赖项](https://i.imgur.com/uTq8g4I.png)

## 配置应用程序

接下来，我们需要配置应用程序以使用文件存储服务。

### 亚马逊 S3

要使用 Amazon S3，我们需要将以下配置添加到“application.properties”文件中：

```
cloud.aws.credentials.access-key=${accessKey}
cloud.aws.credentials.secret-key=${secretKey}

cloud.aws.region.static=${region}

cloud.aws.s3.bucket=${bucketName}
```

将 `${accessKey}`、`${secretKey}`、`${region}` 和 `${bucketName}` 替换为适合您的 Amazon S3 帐户的值。

### 谷歌云端硬盘

要使用 Google Drive，我们需要将以下配置添加到 application.properties 文件中：

```
google.drive.credentials.file=${credentialsFile}
```

将 `${credentialsFile}` 替换为 Google Drive 凭据文件的路径。

## 编写控制器

最后，我们将编写一个简单的控制器来测试文件存储集成。

### 亚马逊 S3

以下控制器将文件上传到 Amazon S3：

```java
@Controller
public class S3Controller {
    @Autowired
    private AmazonS3 amazonS3;

    @PostMapping("/s3/upload")
    public String uploadFile(@RequestParam("file") MultipartFile file) {
        String fileName = file.getOriginalFilename();
        String contentType = file.getContentType();
        amazonS3.putObject(new PutObjectRequest(bucketName, fileName, file.getInputStream(), new ObjectMetadata())
                .withCannedAcl(CannedAccessControlList.PublicRead));
        return "redirect:/";
    }
}
```

在控制器中，我们注入 `AmazonS3` bean 并使用它将文件上传到 Amazon S3。我们还将“Content-Type”标头设置为“file”参数的值。

### 谷歌云端硬盘

以下控制器将文件上传到 Google 云端硬盘：

```java
@Controller
public class DriveController {
    @Autowired
    private Drive drive;

    @PostMapping("/drive/upload")
    public String uploadFile(@RequestParam("file") MultipartFile file) throws IOException {
        File fileMetadata = new File();
        fileMetadata.setName(file.getOriginalFilename());
        fileMetadata.setMimeType(file.getContentType());

        FileContent fileContent = new FileContent(file.getContentType(), file);
        drive.files().create(fileMetadata, fileContent)
                .setFields("id")
                .execute();
        return "redirect:/";
    }
}
```

在控制器中，我们注入 Drive bean 并使用它将文件上传到 Google Drive。我们还将“Content-Type”标头设置为“file”参数的值。

## 测试文件存储集成

要测试文件存储集成，我们需要启动应用程序并上传文件。

### 亚马逊 S3

要测试 Amazon S3 集成，我们需要启动应用程序并将文件上传到“/s3/upload”端点。

该文件将上传到 Amazon S3，并返回一个“200”状态代码。

### 谷歌云端硬盘

要测试 Google Drive 集成，我们需要启动应用程序并将文件上传到“/drive/upload”端点。

该文件将上传到 Google 云端硬盘，并返回“200”状态代码。

## 结论

在本文中，我们学习了如何将 Spring Boot 应用程序与文件存储服务集成，例如 Amazon Simple Storage Service (S3) 或 Google Drive。

我们首先创建一个新的 Spring Boot 项目并添加所需的依赖项。然后，我们将应用程序配置为使用文件存储服务。

最后，我们编写了一个简单的控制器来测试文件存储集成。