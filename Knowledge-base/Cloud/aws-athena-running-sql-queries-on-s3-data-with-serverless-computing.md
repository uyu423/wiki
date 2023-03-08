---
title: AWS Athena: 서버리스 컴퓨팅으로 S3 데이터에서 SQL 쿼리 실행
description: 
published: true
date: 2023-01-31T08:57:38.605Z
tags: 
editor: markdown
dateCreated: 2023-01-31T08:57:36.969Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [AWS Athena: Running SQL Queries on S3 Data with Serverless Computing***English** version of this document is available*](/en/Knowledge-base/Cloud/aws-athena-running-sql-queries-on-s3-data-with-serverless-computing)
{.links-list}
 

# AWS Athena: 서버리스 컴퓨팅으로 S3 데이터에서 SQL 쿼리 실행

# # 소개

클라우드 컴퓨팅의 가장 큰 장점 중 하나는 수요에 따라 서비스를 확장하거나 축소할 수 있다는 것입니다. 이는 연중 특정 시기에 사용량이 급증하는 비즈니스에 특히 중요합니다. 서버리스 컴퓨팅은 클라우드 공급자가 서버를 실행하고 고객이 사용량에 따라 요금을 지불하는 클라우드 컴퓨팅 실행 모델입니다.

AWS Athena는 표준 SQL을 사용하여 Amazon S3의 데이터를 쉽게 분석할 수 있는 서버리스 대화형 쿼리 서비스입니다. Athena는 사용하기 쉽습니다. 인프라를 설정하거나 관리할 필요가 없습니다. 데이터는 S3에 저장되므로 가용성과 내구성이 뛰어납니다. Athena는 쿼리를 병렬로 실행하여 자동으로 확장하므로 대규모 데이터 세트와 복잡한 쿼리가 있는 경우에도 결과가 빠릅니다.

이 기사에서는 AWS Athena를 사용하여 S3에 저장된 데이터를 설정하고 쿼리하는 방법을 살펴보겠습니다. 또한 Athena 사용의 이점과 단점에 대해서도 살펴보겠습니다.

# # AWS Athena 설정

Athena를 사용하기 전에 AWS에서 몇 가지를 설정해야 합니다.

먼저 데이터를 저장할 S3 버킷을 생성해야 합니다. AWS Management 콘솔을 통해 이 작업을 수행하거나 다음 AWS CLI 명령을 사용할 수 있습니다.

```
aws s3 mb s3://{bucket-name}
```

{bucket-name}을 버킷 이름으로 바꿉니다.

다음으로 Athena에서 데이터베이스와 테이블을 생성해야 합니다. Athena는 Apache Hive 메타스토어를 사용하여 데이터베이스 및 테이블에 대한 정보를 저장합니다.

AWS Management 콘솔을 사용하여 데이터베이스와 테이블을 생성하거나 다음 Athena 쿼리 편집기 명령을 사용할 수 있습니다.

```sql
CREATE DATABASE {database-name};

CREATE TABLE {table-name}
(
  {column-name} {data-type}
)
ROW FORMAT SERDE 'org.apache.hive.hcatalog.data.JsonSerDe'
WITH SERDEPROPERTIES (
  'serialization.format' = '1'
)
STORED AS {file-format};
```

다음을 교체합니다.

- {database-name}: 데이터베이스 이름
- {table-name}: 테이블 이름
- {column-name}: 열 이름
- {data-type}: 열의 데이터 유형
- {file-format}: 데이터의 파일 형식(예: 'TEXTFILE', 'PARQUET' 등)

데이터베이스와 테이블을 만든 후에는 데이터를 테이블에 로드해야 합니다. AWS Management 콘솔을 사용하거나 다음 AWS CLI 명령을 사용할 수 있습니다.

```
aws s3 cp {s3-path} {local-path} --recursive
```

다음을 교체합니다.

- {s3-path}: S3의 데이터 경로(예: s3://mybucket/data/)
- {local-path}: 데이터를 복사하려는 로컬 디렉토리의 경로

# # Athena로 데이터 쿼리

이제 데이터가 설정되었으므로 Athena로 쿼리를 시작할 수 있습니다. AWS Management Console을 사용하거나 Athena 쿼리 편집기를 사용하여 이 작업을 수행할 수 있습니다.

Athena 쿼리 편집기를 사용하려면 편집기를 열고 쿼리할 데이터베이스와 테이블을 선택합니다. 그런 다음 쿼리 편집기에 SQL 쿼리를 입력하고 쿼리 실행을 클릭합니다.

Athena가 쿼리를 실행하고 결과를 반환합니다.

나중에 사용할 수 있도록 쿼리를 저장할 수도 있습니다. 이렇게 하려면 저장하려는 쿼리를 선택하고 저장 버튼을 클릭합니다. 쿼리 이름과 설명을 입력하고 저장을 클릭합니다.

# # Athena 사용의 이점

다음을 포함하여 Athena를 사용하면 많은 이점이 있습니다.

- 아테나는 사용하기 쉽습니다. 인프라를 설정하거나 관리할 필요가 없습니다.
- 데이터는 S3에 저장되므로 가용성과 내구성이 뛰어납니다.
- Athena는 쿼리를 병렬로 실행하여 자동으로 확장되므로 대규모 데이터 세트와 복잡한 쿼리가 있는 경우에도 결과가 빠릅니다.
- Athena는 서버리스이므로 실행한 쿼리에 대해서만 비용을 지불합니다. 용량 계획이나 서버 관리에 대해 걱정할 필요가 없습니다.

# # Athena 사용의 단점

Athena 사용에는 다음과 같은 몇 가지 단점도 있습니다.

- Athena는 실시간 데이터 분석이 필요한 사용 사례에는 적합하지 않습니다. S3의 데이터는 일반적으로 몇 분 또는 몇 시간마다 업데이트되므로 Athena 쿼리는 데이터가 업데이트된 직후에 결과를 반환하지 않습니다.
- Athena는 대기 시간이 매우 짧은 데이터 분석이 필요한 사용 사례에는 적합하지 않습니다. S3의 데이터는 일반적으로 몇 분 또는 몇 시간마다 업데이트되므로 Athena 쿼리는 데이터가 업데이트된 직후에 결과를 반환하지 않습니다.
- Athena는 높은 처리량 데이터 분석이 필요한 사용 사례에 적합하지 않습니다. S3의 데이터는 일반적으로 몇 분 또는 몇 시간마다 업데이트되므로 Athena 쿼리는 데이터가 업데이트된 직후에 결과를 반환하지 않습니다.

# # 결론

이 기사에서는 AWS Athena를 사용하여 S3에 저장된 데이터를 설정하고 쿼리하는 방법을 살펴보았습니다. 또한 Athena 사용의 몇 가지 이점과 단점도 살펴보았습니다.