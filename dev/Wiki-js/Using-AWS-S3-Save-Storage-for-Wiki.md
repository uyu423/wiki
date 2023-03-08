---
title: Wiki.js 2.x 에서 AWS S3 를 저장 스토리지로 사용하기
description: 
published: true
date: 2023-02-17T17:59:53.181Z
tags: aws, wikijs
editor: markdown
dateCreated: 2022-12-01T13:45:14.526Z
---

> 공식 문서에도 wiki.js 2.x 의 AWS S3 Storage 설정에 대한 설명이 없어 추가한다.

## AWS S3 생성 (public)

- https://s3.console.aws.amazon.com/s3/home 에서 적당한 이름으로 S3 Bucket 을 생성한다.
- 생성시 ACL 설정을 off 한다.
- 별도의 `버킷 정책` 으로 public 버킷을 만들 필요는 없다.

![스크린샷_2022-12-01_오후_10.35.34.png](/스크린샷_2022-12-01_오후_10.35.34.png =70%x)

## wiki.js Storage 설정

  
> **AWS Access Key Tips**
> AWS Root 계정이 아닌 별도의 IAM 계정(non-login)을 만들고, `AmazonS3FullAccess` 권한을 준다.
> 생성한 IAM 계정의 Access Key, Secret 을 사용하면 안전하다.
{.is-info}

### Amazon S3 로 설정

![스크린샷_2022-12-01_오후_10.41.59.png](/스크린샷_2022-12-01_오후_10.41.59.png =50%x)

- `Wiki.js Admin - Storage` 설정으로 들어간다.
- Storage 로 `AWS S3` 을 선택한다.

![스크린샷_2022-12-01_오후_10.38.46.png](/스크린샷_2022-12-01_오후_10.38.46.png =800x)

- 위와 같이 구성한다.
  - **Region**: S3 Bucket 이 위치한 region code (ex. ap-northeast-2)
  - **Unique bucket name**: AWS S3에 생성된 Public bucket 이름
  - **Access Key ID**: S3 사용 가능한 Access Key ID
  - **Access Key Secret**: S3 사용 가능한 Access Key Secret

### S3 Generic 으로 설정

![스크린샷_2022-12-01_오후_10.42.04.png](/스크린샷_2022-12-01_오후_10.42.04.png =50%x)



![스크린샷_2022-12-01_오후_10.26.37.png](/스크린샷_2022-12-01_오후_10.26.37.png =800x)

- 위와 같이 구성한다.
  - **Endpoint URI**: `https://s3-[your-region-code].amazonaws.com
  - **Unique bucket name**: AWS S3에 생성된 Public bucket 이름
  - **Access Key ID**: S3 사용 가능한 Access Key ID
  - **Access Key Secret**: S3 사용 가능한 Access Key Secret


---

![스크린샷_2022-12-01_오후_10.26.56.png](/스크린샷_2022-12-01_오후_10.26.56.png =50%x)

- `Export All` 기능을 사용하여 AWS S3에 wiki.js의 문서가 정상적으로 export 되는지 확인할 수 있다.