---
title: 사례 연구: AWS에서 간단한 전자 상거래 서비스 개발 및 시작
description: 
published: true
date: 2023-02-04T11:18:08.721Z
tags: 
editor: markdown
dateCreated: 2023-02-04T11:18:07.008Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Case Study: Developing and Launching a Simple e-Commerce Service on AWS***English** document is available*](/en/Knowledge-base/Cloud/case-study-developing-and-launching-a-simple-e-commerce-service-on-aws)
{.links-list}


# 사례 연구: AWS에서 간단한 전자 상거래 서비스 개발 및 시작

이 사례 연구에서는 AWS에서 간단한 전자 상거래 서비스를 개발하고 시작하는 방법을 보여줍니다. 서비스의 아키텍처와 사용되는 다양한 AWS 서비스에 대해 살펴보겠습니다. 시작하는 데 도움이 되는 몇 가지 코드 예제도 제공합니다.

## 아키텍처

우리가 개발할 e-Commerce 서비스는 웹 프런트엔드와 백엔드 데이터베이스로 구성된 단순한 서비스입니다. 웹 프런트 엔드는 PHP 프로그래밍 언어를 사용하여 개발되고 백엔드 데이터베이스는 MySQL입니다.

![전자상거래 서비스 아키텍처](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/architecture.png)

웹 프런트 엔드는 Amazon EC2 인스턴스에서 호스팅되며 Amazon CloudFront 배포를 통해 액세스됩니다. CloudFront는 웹 사이트의 정적 콘텐츠(예: 이미지, CSS 및 JavaScript 파일)를 캐시하고 짧은 지연 시간으로 사용자에게 전달하는 콘텐츠 전송 네트워크(CDN)입니다.

백엔드 데이터베이스는 Amazon RDS에서 호스팅되며 제품 및 주문 데이터를 저장하는 데 사용됩니다. RDS는 클라우드에서 관계형 데이터베이스를 쉽게 설정, 운영 및 확장할 수 있게 해주는 관리형 관계형 데이터베이스 서비스입니다.

## 사용된 AWS 서비스

이 사례 연구에서는 다음 AWS 서비스가 사용됩니다.

- 아마존 EC2
- 아마존 클라우드프론트
- 아마존 RDS
- 아마존 S3

## 백엔드 데이터베이스 설정

백엔드 데이터베이스를 설정하는 것으로 시작하겠습니다. 우리는 MySQL용 Amazon RDS를 사용할 것입니다.

먼저 새 RDS 인스턴스를 만듭니다. MySQL 엔진과 db.t2.micro 인스턴스 클래스를 선택하겠습니다.

![새 RDS 인스턴스 생성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-01.png)

다음으로 인스턴스에 대한 설정을 구성합니다. 인스턴스에 이름을 지정하고 MySQL 5.6.x 데이터베이스 엔진을 선택한 다음 db.t2.micro 인스턴스 클래스를 선택합니다.

![RDS 인스턴스 구성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-02.png)

다음으로 새 데이터베이스를 만듭니다. 데이터베이스에 이름을 지정하고 MySQL 5.6.x 데이터베이스 엔진을 선택합니다.

![새 데이터베이스 생성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-03.png)

이제 데이터베이스가 생성되었으므로 사용자를 생성하고 데이터베이스에 대한 사용자 액세스 권한을 부여해야 합니다. 사용자 이름이 "ecommerce"이고 비밀번호가 "password"인 사용자를 생성합니다.

![새 사용자 만들기](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-04.png)

다음으로 사용자에게 데이터베이스에 대한 액세스 권한을 부여합니다. "전자상거래" 데이터베이스와 "전자상거래" 사용자를 선택하고 "추가" 버튼을 클릭합니다.

![데이터베이스에 대한 액세스 권한 부여](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/rds-05.png)

## 웹 프런트 엔드 설정

백엔드 데이터베이스가 설정되었으므로 이제 웹 프런트엔드를 설정해야 합니다. 이를 위해 Amazon EC2를 사용할 것입니다.

먼저 새 EC2 인스턴스를 생성합니다. Amazon Linux AMI와 t2.micro 인스턴스 유형을 선택하겠습니다.

![새 EC2 인스턴스 생성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/ec2-01.png)

다음으로 인스턴스에 대한 설정을 구성합니다. 인스턴스에 이름을 지정하고 Amazon Linux AMI를 선택한 다음 t2.micro 인스턴스 유형을 선택합니다.

![EC2 인스턴스 구성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/ec2-02.png)

이제 인스턴스가 생성되었으므로 인스턴스에 SSH로 연결해야 합니다. 인스턴스를 만들 때 다운로드한 개인 키를 사용합니다.

![EC2 인스턴스에 대한 SSH](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/ec2-03.png)

인스턴스에 로그인하면 Apache 웹 서버, PHP 및 MySQL 클라이언트를 설치해야 합니다. yum 패키지 관리자를 사용하여 이 작업을 수행합니다.

```bash
$ sudo yum install -y httpd24 php70 mysql56-client
```

다음으로 Apache 웹 서버를 시작합니다.

```bash
$ sudo service httpd start
```

이제 웹 서버가 가동되어 실행 중이므로 새 PHP 파일을 만들어야 합니다. 이 파일을 "index.php"라고 하고 "/var/www/html" 디렉토리에 넣습니다.

```php
<?php
  echo "Hello, world!";
?>
```

이제 "/etc/httpd/conf/httpd.conf" 파일을 편집하고 다음 행의 주석을 제거해야 합니다.

```apache
LoadModule rewrite_module modules/mod_rewrite.so
```

다음으로 Apache 웹 서버를 다시 시작합니다.

```bash
$ sudo service httpd restart
```

이제 새로운 MySQL 사용자를 생성해야 합니다. 이전에 생성한 "전자상거래" 사용자를 사용하겠습니다. 사용자에게 "전자상거래" 데이터베이스에 대한 액세스 권한을 부여합니다.

```sql
GRANT ALL ON ecommerce.* TO 'ecommerce'@'localhost' IDENTIFIED BY 'password';
```

이제 사용자가 생성되었으므로 데이터를 데이터베이스로 가져와야 합니다. GitHub 리포지토리에 포함된 "products.sql" 파일을 사용합니다.

```bash
$ mysql -u ecommerce -p ecommerce < products.sql
```

## 애플리케이션 테스트

이제 응용 프로그램이 설정되었으므로 모든 것이 예상대로 작동하는지 테스트해야 합니다. 웹 브라우저를 통해 애플리케이션에 액세스하여 시작하겠습니다.

![애플리케이션 테스트](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/testing-01.png)

보시다시피 응용 프로그램이 예상대로 작동합니다. 제품 목록을 볼 수 있고 장바구니에 항목을 추가할 수 있습니다.

![애플리케이션 테스트](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/testing-02.png)

## 애플리케이션 실행

이제 응용 프로그램이 실행 중이므로 시작해야 합니다. Amazon CloudFront 배포를 생성하여 이를 수행합니다.

먼저 새로운 CloudFront 배포를 생성합니다. "웹" 전달 방법과 "가져오기" HTTP 방법을 선택하겠습니다.

![새 CloudFront 배포 생성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-01.png)

다음으로 배포 설정을 구성합니다. 배포에 이름을 지정하고 "웹" 전달 방법을 선택한 다음 "가져오기" HTTP 방법을 선택합니다.

![CloudFront 배포 구성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-02.png)

이제 새 원본을 만들어야 합니다. "Custom Origin" 유형을 선택하고 EC2 인스턴스의 URL을 입력합니다.

![새 오리진 생성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-03.png)

다음으로 오리진에 대한 설정을 구성합니다. 오리진에 이름을 지정하고 "Custom Origin" 유형을 선택한 다음 EC2 인스턴스의 URL을 입력합니다.

![오리진 설정](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-04.png)

이제 새로운 기본 캐시 동작을 만들어야 합니다. "기본(*)" 경로 패턴을 선택하고 전달 헤더에 대해 "모두 허용" 옵션을 선택합니다.

![새 기본 캐시 동작 생성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-05.png)

다음으로 기본 캐시 동작에 대한 설정을 구성합니다. "기본(*)" 경로 패턴을 선택하고 전달 헤더에 대해 "모두 허용" 옵션을 선택합니다.

![기본 캐시 동작 구성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-06.png)

이제 새 오류 페이지를 만들어야 합니다. "404" 오류 코드를 선택하고 오류 페이지의 URL을 입력합니다.

![새 오류 페이지 생성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-07.png)

다음으로 오류 페이지에 대한 설정을 구성합니다. "404" 오류 코드를 선택하고 오류 페이지의 URL을 입력합니다.

![오류 페이지 구성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-08.png)

이제 새 SSL 인증서를 만들어야 합니다. "사용자 지정 인증서" 옵션을 선택하고 웹 사이트의 도메인 이름을 입력합니다.

![새 SSL 인증서 생성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-09.png)

다음으로 SSL 인증서에 대한 설정을 구성합니다. "사용자 지정 인증서" 옵션을 선택하고 웹 사이트의 도메인 이름을 입력합니다.

![SSL 인증서 구성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-10.png)

이제 새 배포판을 만들어야 합니다. "웹" 전달 방법과 "가져오기" HTTP 방법을 선택하겠습니다.

![새 배포 만들기](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-11.png)

다음으로 배포 설정을 구성합니다. 배포에 이름을 지정하고 "웹" 전달 방법을 선택한 다음 "가져오기" HTTP 방법을 선택합니다.

![배포 구성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-12.png)

이제 새로운 기본 캐시 동작을 만들어야 합니다. "기본(*)" 경로 패턴을 선택하고 전달 헤더에 대해 "모두 허용" 옵션을 선택합니다.

![새 기본 캐시 동작 생성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-13.png)

다음으로 기본 캐시 동작에 대한 설정을 구성합니다. "기본(*)" 경로 패턴을 선택하고 전달 헤더에 대해 "모두 허용" 옵션을 선택합니다.

![기본 캐시 동작 구성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-14.png)

이제 새 오류 페이지를 만들어야 합니다. "404" 오류 코드를 선택하고 오류 페이지의 URL을 입력합니다.

![새 오류 페이지 생성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-15.png)

다음으로 오류 페이지에 대한 설정을 구성합니다. "404" 오류 코드를 선택하고 오류 페이지의 URL을 입력합니다.

![오류 페이지 구성](https://raw.githubusercontent.com/itdevelopmentlearning/simple-ecommerce-on-aws/master/images/cloudfront-16.png)

## 결론

이 사례 연구에서는 AWS에서 간단한 전자 상거래 서비스를 개발하고 시작하는 방법을 보여 주었습니다. 서비스의 아키텍처와 사용되는 다양한 AWS 서비스에 대해 살펴보았습니다. 시작하는 데 도움이 되는 몇 가지 코드 예제도 제공했습니다.