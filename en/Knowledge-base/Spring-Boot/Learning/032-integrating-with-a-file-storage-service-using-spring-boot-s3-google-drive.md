---
title: 032: Integrating with a file storage service using Spring Boot (S3, Google Drive)
description: 
published: true
date: 2023-02-04T00:32:29.737Z
tags: 
editor: markdown
dateCreated: 2023-02-04T00:32:24.619Z
---

- [032: Integración con un servicio de almacenamiento de archivos usando Spring Boot (S3, Google Drive)***Spanish** document is available*](/es/Knowledge-base/Spring-Boot/Learning/032-integrating-with-a-file-storage-service-using-spring-boot-s3-google-drive)
{.links-list}
- [032：使用 Spring Boot（S3、Google Drive）与文件存储服务集成***Chinese Simplified** document is available*](/zh/Knowledge-base/Spring-Boot/Learning/032-integrating-with-a-file-storage-service-using-spring-boot-s3-google-drive)
{.links-list}
- [032: Spring Boot(S3, Google Drive)를 이용한 파일 저장 서비스 연동***Korean** document is available*](/ko/Knowledge-base/Spring-Boot/Learning/032-integrating-with-a-file-storage-service-using-spring-boot-s3-google-drive)
{.links-list}


# 032: Integrating with a file storage service using Spring Boot (S3, Google Drive)

In this post, we'll learn how to integrate a Spring Boot application with a file storage service, such as Amazon Simple Storage Service (S3) or Google Drive.

We'll start by creating a new Spring Boot project and adding the required dependencies. Then, we'll configure the application to use the file storage service.

Finally, we'll write a simple controller to test the file storage integration.

## Creating the Spring Boot project

First, we'll create a new Spring Boot project using the [Spring Initializr](https://start.spring.io/). We'll name the project `file-storage-service-integration`.

![Spring Initializr](https://i.imgur.com/HUjEr9r.png)

We'll select the following dependencies:

* Web - for the web interface
* Cloud AWS - for the Amazon S3 integration
* Cloud GCP - for the Google Drive integration

![Spring Initializr Dependencies](https://i.imgur.com/uTq8g4I.png)

## Configuring the application

Next, we'll need to configure the application to use the file storage service.

### Amazon S3

To use Amazon S3, we'll need to add the following configuration to the `application.properties` file:

```
cloud.aws.credentials.access-key=${accessKey}
cloud.aws.credentials.secret-key=${secretKey}

cloud.aws.region.static=${region}

cloud.aws.s3.bucket=${bucketName}
```

Replace `${accessKey}`, `${secretKey}`, `${region}`, and `${bucketName}` with the appropriate values for your Amazon S3 account.

### Google Drive

To use Google Drive, we'll need to add the following configuration to the `application.properties` file:

```
google.drive.credentials.file=${credentialsFile}
```

Replace `${credentialsFile}` with the path to the Google Drive credentials file.

## Writing the controller

Finally, we'll write a simple controller to test the file storage integration.

### Amazon S3

The following controller will upload a file to Amazon S3:

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

In the controller, we inject the `AmazonS3` bean and use it to upload the file to Amazon S3. We also set the `Content-Type` header to the value of the `file` parameter.

### Google Drive

The following controller will upload a file to Google Drive:

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

In the controller, we inject the `Drive` bean and use it to upload the file to Google Drive. We also set the `Content-Type` header to the value of the `file` parameter.

## Testing the file storage integration

To test the file storage integration, we'll need to start the application and upload a file.

### Amazon S3

To test the Amazon S3 integration, we'll need to start the application and upload a file to the `/s3/upload` endpoint.

The file will be uploaded to Amazon S3 and a `200` status code will be returned.

### Google Drive

To test the Google Drive integration, we'll need to start the application and upload a file to the `/drive/upload` endpoint.

The file will be uploaded to Google Drive and a `200` status code will be returned.

## Conclusion

In this post, we learned how to integrate a Spring Boot application with a file storage service, such as Amazon Simple Storage Service (S3) or Google Drive.

We started by creating a new Spring Boot project and adding the required dependencies. Then, we configured the application to use the file storage service.

Finally, we wrote a simple controller to test the file storage integration.