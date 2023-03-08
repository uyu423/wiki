---
title: 032: Spring Boot(S3, Google Drive)를 이용한 파일 저장 서비스 연동
description: 
published: true
date: 2023-02-04T00:32:26.205Z
tags: 
editor: markdown
dateCreated: 2023-02-04T00:32:24.612Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [032: Integrating with a file storage service using Spring Boot (S3, Google Drive)***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/032-integrating-with-a-file-storage-service-using-spring-boot-s3-google-drive)
{.links-list}


# 032 : Spring Boot(S3, Google Drive)를 이용한 파일 저장 서비스 연동

이 게시물에서는 Spring Boot 애플리케이션을 Amazon Simple Storage Service(S3) 또는 Google 드라이브와 같은 파일 스토리지 서비스와 통합하는 방법을 알아봅니다.

새 Spring Boot 프로젝트를 생성하고 필요한 종속성을 추가하는 것으로 시작하겠습니다. 그런 다음 파일 스토리지 서비스를 사용하도록 애플리케이션을 구성합니다.

마지막으로 파일 저장소 통합을 테스트하기 위해 간단한 컨트롤러를 작성합니다.

## 스프링 부트 프로젝트 생성

먼저 [Spring Initializr](https://start.spring.io/)를 사용하여 새로운 Spring Boot 프로젝트를 생성합니다. 프로젝트 이름을 'file-storage-service-integration'으로 지정합니다.

![스프링 이니셜라이저](https://i.imgur.com/HUjEr9r.png)

다음 종속성을 선택합니다.

* 웹 - 웹 인터페이스용
* Cloud AWS - Amazon S3 통합용
* Cloud GCP - Google 드라이브 통합용

![Spring Initializr 의존성](https://i.imgur.com/uTq8g4I.png)

## 애플리케이션 구성

다음으로 파일 스토리지 서비스를 사용하도록 애플리케이션을 구성해야 합니다.

### 아마존 S3

Amazon S3를 사용하려면 `application.properties` 파일에 다음 구성을 추가해야 합니다.

```
cloud.aws.credentials.access-key=${accessKey}
cloud.aws.credentials.secret-key=${secretKey}

cloud.aws.region.static=${region}

cloud.aws.s3.bucket=${bucketName}
```

`${accessKey}`, `${secretKey}`, `${region}` 및 `${bucketName}`을 Amazon S3 계정에 적합한 값으로 바꿉니다.

### 구글 드라이브

Google 드라이브를 사용하려면 `application.properties` 파일에 다음 구성을 추가해야 합니다.

```
google.drive.credentials.file=${credentialsFile}
```

`${credentialsFile}`을 Google 드라이브 자격 증명 파일의 경로로 바꿉니다.

## 컨트롤러 쓰기

마지막으로 파일 저장소 통합을 테스트하기 위해 간단한 컨트롤러를 작성합니다.

### 아마존 S3

다음 컨트롤러는 Amazon S3에 파일을 업로드합니다.

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

컨트롤러에서 `AmazonS3` 빈을 주입하고 이를 사용하여 파일을 Amazon S3에 업로드합니다. 또한 `Content-Type` 헤더를 `file` 매개변수 값으로 설정합니다.

### 구글 드라이브

다음 컨트롤러는 Google 드라이브에 파일을 업로드합니다.

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

컨트롤러에서 `Drive` 빈을 주입하고 이를 사용하여 Google 드라이브에 파일을 업로드합니다. 또한 `Content-Type` 헤더를 `file` 매개변수 값으로 설정합니다.

## 파일 스토리지 통합 테스트

파일 스토리지 통합을 테스트하려면 애플리케이션을 시작하고 파일을 업로드해야 합니다.

### 아마존 S3

Amazon S3 통합을 테스트하려면 애플리케이션을 시작하고 `/s3/upload` 엔드포인트에 파일을 업로드해야 합니다.

파일이 Amazon S3에 업로드되고 '200' 상태 코드가 반환됩니다.

### 구글 드라이브

Google 드라이브 통합을 테스트하려면 애플리케이션을 시작하고 `/drive/upload` 엔드포인트에 파일을 업로드해야 합니다.

파일이 Google Drive에 업로드되고 `200` 상태 코드가 반환됩니다.

## 결론

이 게시물에서는 Spring Boot 애플리케이션을 Amazon Simple Storage Service(S3) 또는 Google 드라이브와 같은 파일 스토리지 서비스와 통합하는 방법을 배웠습니다.

새로운 Spring Boot 프로젝트를 생성하고 필요한 종속성을 추가하는 것으로 시작했습니다. 그런 다음 파일 스토리지 서비스를 사용하도록 애플리케이션을 구성했습니다.

마지막으로 파일 스토리지 통합을 테스트하기 위해 간단한 컨트롤러를 작성했습니다.