---
title: MongoDB 시작하기: 초보자 가이드
description: 
published: true
date: 2023-03-04T23:32:41.988Z
tags: 
editor: markdown
dateCreated: 2023-03-04T23:32:34.757Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Getting Started with MongoDB: A Beginner's Guide***English** document is available*](/en/Knowledge-base/NoSQL/getting-started-with-mongodb-a-beginner-s-guide)
{.links-list}
## 소개

MongoDB는 확장성, 유연성 및 성능으로 잘 알려진 널리 사용되는 NoSQL 데이터베이스입니다. 신생 기업, 기업 및 정부 기관을 포함한 모든 규모의 조직에서 널리 사용됩니다. MongoDB는 오픈 소스 문서 데이터베이스입니다. 즉, 다양한 구조를 가질 수 있는 유연하고 JSON과 유사한 문서에 데이터를 저장합니다. 따라서 소셜 미디어 플랫폼, 전자 상거래 웹 사이트 및 콘텐츠 관리 시스템과 같이 빠르고 유연한 데이터 모델링이 필요한 애플리케이션에 적합합니다.

## 전제 조건

MongoDB를 시작하기 전에 SQL 및 데이터베이스 설계 원칙을 포함하여 데이터베이스에 대한 기본 지식이 있어야 합니다. 또한 Python, Java 또는 Node.js와 같은 프로그래밍 언어에 익숙해야 합니다. MongoDB는 가장 널리 사용되는 프로그래밍 언어에 대한 드라이버와 라이브러리를 제공하므로 선호하는 언어를 사용하여 데이터베이스와 상호 작용할 수 있습니다.

## 설치

MongoDB는 Windows, macOS 및 Linux에 설치할 수 있으며 운영 체제에 따라 사용 가능한 설치 방법이 다릅니다.

### 윈도우

Windows에 MongoDB를 설치하려면 다음 단계를 따르십시오.

1. [공식 웹사이트](https://www.mongodb.com/try/download/community)에서 MongoDB 설치 프로그램을 다운로드합니다.
2. 설치 프로그램을 실행하고 "완료" 설치 유형을 선택합니다.
3. 기본 설정을 그대로 두고 "설치"를 클릭합니다.
4. 설치가 완료되면 MongoDB를 사용할 수 있습니다.

### 맥 OS

macOS에 MongoDB를 설치하려면 다음 단계를 따르십시오.

1. 터미널에서 다음 명령을 실행하여 Homebrew를 설치합니다.

   ```/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"```
   
2. 터미널에서 다음 명령을 실행하여 MongoDB를 설치합니다.

   ```brew install mongodb-community```
   
3. 터미널에서 다음 명령을 실행하여 MongoDB 서비스를 시작합니다.

   ```양조 서비스 시작 mongodb-community```
   
### 리눅스

Linux에 MongoDB를 설치하려면 다음 단계를 따르십시오.

1. 다음 명령을 실행하여 패키지 관리자에 MongoDB 리포지토리를 추가합니다.

   ```sudo apt-get install gnupg```
   
   ```wget -qO - https://www.mongodb.org/static/pgp/server-4.4.asc | sudo apt-key 추가 -```
   
   ```echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu $(lsb_release -cs)/mongodb-org/4.4 multiverse" | sudo 티 /etc/apt/sources.list.d/mongodb-org-4.4.list```
   
2. 터미널에서 다음 명령을 실행하여 MongoDB를 설치합니다.

   ```sudo apt-get 업데이트```
   
   ```sudo apt-get install -y mongodb-org```
   
3. 터미널에서 다음 명령을 실행하여 MongoDB 서비스를 시작합니다.

   ```sudo systemctl start mongod```
   
## 시작하기

머신에 MongoDB가 설치되면 사용을 시작할 수 있습니다. 첫 번째 단계는 데이터베이스와 컬렉션을 만드는 것입니다. MongoDB에서 데이터베이스는 컬렉션의 컨테이너이고 컬렉션은 문서 그룹입니다.

데이터베이스와 컬렉션을 만들려면 데이터베이스와 상호 작용할 수 있는 명령줄 인터페이스인 MongoDB 셸을 사용할 수 있습니다.

### 데이터베이스 생성

데이터베이스를 생성하려면 터미널에서 다음 명령을 실행하여 MongoDB 셸을 엽니다.

```mongo```

This will open the MongoDB shell prompt. From here, you can create a database by running the following command:

```mydatabase 사용```

이렇게 하면 "mydatabase"라는 데이터베이스가 생성됩니다. 데이터베이스가 존재하지 않으면 MongoDB가 자동으로 생성합니다.

### 컬렉션 만들기

컬렉션을 생성하려면 `db.createCollection()` 메서드를 사용할 수 있습니다. 예를 들어 "mycollection"이라는 컬렉션을 만들려면 다음 명령을 실행합니다.

```db.createCollection("mycollection")```

This will create a collection called "mycollection" in the "mydatabase" database. 

### Inserting Data

To insert data into a collection, you can use the `db.collection.insert()` method. For example, to insert a document into the "mycollection" collection, run the following command:

```db.mycollection.insert({"name": "John", "age": 30})```

이렇게 하면 "이름" 필드가 "John"으로 설정되고 "나이" 필드가 30으로 설정된 문서가 삽입됩니다.

### 데이터 쿼리

컬렉션에서 데이터를 쿼리하려면 `db.collection.find()` 메서드를 사용할 수 있습니다. 예를 들어 "mycollection" 컬렉션에서 모든 문서를 찾으려면 다음 명령을 실행합니다.

```db.mycollection.find()```

This will return all documents in the "mycollection" collection. 

### Updating Data

To update data in a collection, you can use the `db.collection.update()` method. For example, to update the document with the "name" field set to "John" and set the "age" field to 35, run the following command:

```db.mycollection.update({"name": "John"}, {"$set": {"age": 35}})```

이렇게 하면 "이름" 필드가 "John"으로 설정된 문서가 업데이트되고 "나이" 필드가 35로 설정됩니다.

### 데이터 삭제

컬렉션에서 데이터를 삭제하려면 `db.collection.remove()` 메서드를 사용할 수 있습니다. 예를 들어 "이름" 필드가 "John"으로 설정된 문서를 삭제하려면 다음 명령을 실행합니다.

```db.mycollection.remove({"이름": "John"})```

이렇게 하면 "이름" 필드가 "John"으로 설정된 문서가 삭제됩니다.

## 결론

이 기사에서는 MongoDB를 시작하는 기본 사항을 다뤘습니다. 다양한 운영 체제에서의 설치 프로세스를 살펴보고 데이터베이스 생성, 컬렉션, 데이터 삽입, 데이터 쿼리, 데이터 업데이트 및 데이터 삭제 방법을 시연했습니다. MongoDB는 광범위한 애플리케이션에 사용할 수 있는 강력한 도구이며 이 기사가 이 기술을 사용하기 위한 좋은 출발점을 제공했기를 바랍니다.

## 외부 리소스

- [MongoDB 문서](https://docs.mongodb.com/)
- [몽고DB대학교](https://university.mongodb.com/)
- [MongoDB 튜토리얼](https://www.tutorialspoint.com/mongodb/index.htm)