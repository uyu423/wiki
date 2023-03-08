---
title: MySQL 08: 실제 비즈니스 문제에 대한 SQL: 고객 세분화 및 제품 분석
description: 
published: true
date: 2023-02-06T14:32:48.801Z
tags: 
editor: markdown
dateCreated: 2023-02-06T14:32:47.100Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [MySQL 08: SQL for real-world business problems: Customer segmentation and product analysis***English** document is available*](/en/Knowledge-base/mysql-for-planner-marketers/Learning/mysql-08-sql-for-real-world-business-problems-customer-segmentation-and-product-analysis)
{.links-list}


MySQL 08: 실제 비즈니스 문제에 대한 SQL: 고객 세분화 및 제품 분석

이 게시물에서는 SQL을 사용하여 실제 비즈니스 문제를 해결하는 방법을 배웁니다. 기업이 직면하는 두 가지 일반적인 문제인 고객 세분화와 제품 분석을 다룰 것입니다.

고객 세분화는 공통된 특성에 따라 고객을 그룹으로 나누는 프로세스입니다. 이는 기업이 마케팅 및 판매 노력을 특정 고객 그룹에 맞게 조정할 수 있기 때문에 중요합니다.

상품 분석은 상품의 판매 데이터를 이해하는 과정입니다. 이는 기업이 제품 개발, 가격 책정 및 재고 관리에 대해 정보에 입각한 결정을 내릴 수 있기 때문에 중요합니다.

이 게시물에서는 MySQL 데이터베이스를 사용합니다. MySQL은 무료 오픈 소스 데이터베이스 관리 시스템입니다. 웹 응용 프로그램에 널리 사용되며 Facebook, Twitter 및 YouTube를 포함하여 세계에서 가장 큰 일부 웹 사이트에서 사용됩니다.

시작하려면 데이터베이스를 만들어야 합니다. MySQL 콘솔이나 phpMyAdmin과 같은 GUI 도구를 사용하여 이 작업을 수행할 수 있습니다. 데이터베이스 이름을 "business"로 지정합니다.

다음으로 "고객"과 "제품"이라는 두 개의 테이블을 만들어야 합니다.

"고객" 테이블은 고객에 대한 정보를 저장합니다. 다음 열을 포함해야 합니다.

* customer_id: 고객의 고유 ID입니다.
* 이름: 고객의 이름입니다.
* 이메일: 고객의 이메일 주소입니다.
* date_of_birth: 고객의 생년월일.
* 성별: 고객의 성별입니다.

"제품" 테이블은 제품에 대한 정보를 저장합니다. 다음 열을 포함해야 합니다.

* product_id: 제품의 고유 ID입니다.
* 이름: 제품의 이름입니다.
* 가격: 제품의 가격입니다.
* 카테고리: 상품의 카테고리입니다.
* release_date: 제품의 출시일.

이제 데이터베이스와 테이블이 설정되었으므로 데이터 추가를 시작할 수 있습니다.

"고객" 테이블부터 시작하겠습니다. 데이터베이스에 세 명의 고객을 추가합니다.

* 고객 ID: 1
* 이름: 존 스미스
* 이메일: john@example.com
* 생년월일: 2000년 1월 1일
* 성별 남성

* 고객 ID: 2
* 이름: Jane Doe
* 이메일: jane@example.com
* 생년월일: 2001년 2월 2일
* 성별 여성

* 고객 ID: 3
* 이름: John Doe
* 이메일: john@example.com
* 생년월일: 2000년 1월 1일
* 성별 남성

다음으로 "products" 테이블에 데이터를 추가합니다. 데이터베이스에 세 가지 제품을 추가합니다.

* product_id: 1
* 이름: 제품 1
* 가격: 10
* 카테고리: 카테고리 1
* 출시일: 2020년 1월 1일

* product_id: 2
* 이름: 제품 2
* 가격: 20
* 카테고리: 카테고리 2
* 출시일: 2021년 2월 2일

* product_id: 3
* 이름: 제품 3
* 가격: 30
* 카테고리: 카테고리 3
* 출시일: 2022년 3월 3일

이제 데이터가 있으므로 쿼리를 시작할 수 있습니다.

"customers" 테이블에서 모든 데이터를 가져오는 간단한 쿼리부터 시작하겠습니다.

```mysql
SELECT * FROM customers;
```

이 쿼리는 "customers" 테이블의 모든 열과 행을 반환합니다.

다음으로 "customers" 테이블에서 특정 데이터를 가져오는 쿼리를 작성합니다. 예를 들어, 여성인 모든 고객을 얻고자 할 수 있습니다.

```mysql
SELECT * FROM customers
WHERE gender = "Female";
```

이 쿼리는 성별이 "여성"인 "고객" 테이블의 모든 열과 행을 반환합니다.

MySQL GROUP BY 절을 사용하여 데이터를 그룹화할 수도 있습니다. 예를 들어 고객을 성별로 그룹화할 수 있습니다.

```mysql
SELECT gender, COUNT(*) FROM customers
GROUP BY gender;
```

이 쿼리는 각 성별에 대한 고객 수를 반환합니다.

MySQL ORDER BY 절을 사용하여 데이터를 정렬할 수도 있습니다. 예를 들어 고객을 이름으로 주문할 수 있습니다.

```mysql
SELECT * FROM customers
ORDER BY name;
```

이 쿼리는 "customers" 테이블의 모든 열과 행을 이름순으로 반환합니다.

이제 "customers" 테이블을 쿼리하는 방법을 배웠으므로 "products" 테이블로 이동하겠습니다.

"products" 테이블에서 모든 데이터를 가져오는 간단한 쿼리부터 시작하겠습니다.

```mysql
SELECT * FROM products;
```

이 쿼리는 "product" 테이블의 모든 열과 행을 반환합니다.

다음으로 "product" 테이블에서 특정 데이터를 가져오는 쿼리를 작성합니다. 예를 들어 "카테고리 1" 범주에 있는 모든 제품을 가져오려고 할 수 있습니다.

```mysql
SELECT * FROM products
WHERE category = "category 1";
```

이 쿼리는 범주가 "범주 1"인 "제품" 테이블의 모든 열과 행을 반환합니다.

MySQL GROUP BY 절을 사용하여 데이터를 그룹화할 수도 있습니다. 예를 들어 제품을 범주별로 그룹화할 수 있습니다.

```mysql
SELECT category, COUNT(*) FROM products
GROUP BY category;
```

이 쿼리는 각 범주의 제품 수를 반환합니다.

MySQL ORDER BY 절을 사용하여 데이터를 정렬할 수도 있습니다. 예를 들어 제품을 가격별로 주문할 수 있습니다.

```mysql
SELECT * FROM products
ORDER BY price;
```

이 쿼리는 "product" 테이블의 모든 열과 행을 가격순으로 반환합니다.

마지막으로 각 범주에 있는 제품의 평균 가격을 가져오는 쿼리를 작성합니다.

```mysql
SELECT category, AVG(price) FROM products
GROUP BY category;
```

이 쿼리는 각 범주에 있는 제품의 평균 가격을 반환합니다.

그게 다야! 이제 SQL을 사용하여 실제 비즈니스 문제를 해결하는 방법을 배웠습니다.