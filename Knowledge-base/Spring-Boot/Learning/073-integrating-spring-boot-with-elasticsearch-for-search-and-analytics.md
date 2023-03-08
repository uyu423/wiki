---
title: 073: 검색 및 분석을 위해 Elasticsearch와 Spring Boot 통합
description: 
published: true
date: 2023-02-02T04:43:40.776Z
tags: 
editor: markdown
dateCreated: 2023-02-02T04:43:39.050Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [073: Integrating Spring Boot with Elasticsearch for Search and Analytics***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/073-integrating-spring-boot-with-elasticsearch-for-search-and-analytics)
{.links-list}


# 소개

Elasticsearch는 데이터를 쉽게 탐색할 수 있는 강력한 오픈 소스 검색 및 분석 엔진입니다. Spring Boot는 독립 실행형 프로덕션 등급 Spring 기반 애플리케이션을 쉽게 만들 수 있는 인기 있는 Java 애플리케이션 프레임워크입니다.

이 게시물에서는 검색 및 분석을 위해 Spring Boot를 Elasticsearch와 통합하는 방법을 보여줍니다. 먼저 Spring Boot 애플리케이션을 만들고 필요한 종속성을 추가합니다. 그런 다음 Elasticsearch 인덱스를 생성하고 일부 데이터를 추가합니다. 마지막으로 Elasticsearch API를 사용하여 인덱스에서 데이터를 검색하고 집계하는 Spring Boot 애플리케이션을 작성합니다.

# 전제 조건

이 게시물을 따라하려면 다음이 필요합니다.

- JDK 8 이상
- Gradle 4.0 이상

# 스프링 부트 애플리케이션 생성

Spring Boot 애플리케이션을 만드는 것부터 시작하겠습니다. Spring Initializr를 사용하여 기본 프로젝트 구조를 생성합니다. http://start.spring.io/로 이동하여 다음 옵션을 선택합니다.

- 프로젝트: Gradle 프로젝트
- 언어: 자바
- 스프링 부트 버전: 2.0.3
- 프로젝트 메타데이터:
  - 그룹: com.example
  - 아티팩트: spring-boot-elasticsearch
  - 이름: Spring Boot Elasticsearch
  - 설명: Elasticsearch와 연동되는 Spring Boot 애플리케이션
  - 패키지 이름: com.example.springbootelasticsearch
  - 포장: 항아리
  - 자바 버전: 8
  - 종속성: 웹, 롬복

프로젝트 아카이브를 다운로드하려면 "프로젝트 생성"을 클릭하십시오. 아카이브를 추출하고 프로젝트를 원하는 IDE로 가져옵니다.

# 종속성 추가

다음으로 프로젝트에 필요한 종속성을 추가해야 합니다. 다음 종속성이 필요합니다.

- Spring Data Elasticsearch: Spring 애플리케이션에서 Elasticsearch 지원 제공
- Elasticsearch: Elasticsearch 엔진 자체
- Lombok: 상용구 코드를 생성할 수 있는 라이브러리

`build.gradle` 파일의 `dependencies` 섹션에 다음 종속성을 추가합니다.

```groovy
dependencies {
    compile('org.springframework.boot:spring-boot-starter-data-elasticsearch')
    compile('org.elasticsearch:elasticsearch:6.3.2')
    compileOnly('org.projectlombok:lombok')
    testCompile('org.springframework.boot:spring-boot-starter-test')
}
```

# 엘라스틱서치 설정

다음으로 Elasticsearch를 구성해야 합니다. 기본적으로 Spring Boot는 `http://localhost:9200`에서 Elasticsearch 인스턴스를 찾습니다. 다른 호스트 또는 포트에서 실행 중인 Elasticsearch가 있는 경우 `application.properties`에서 `spring.data.elasticsearch.cluster-nodes` 및 `spring.data.elasticsearch.cluster-name` 속성을 설정하여 구성할 수 있습니다. 파일. 예를 들어:

```properties
spring.data.elasticsearch.cluster-nodes=localhost:9300
spring.data.elasticsearch.cluster-name=my-cluster
```

# Elasticsearch 인덱스 생성

Elasticsearch 색인은 유사한 특성을 가진 문서 모음입니다. 인덱스를 관계형 데이터베이스의 테이블로 생각할 수 있습니다. 테이블에 데이터를 삽입하기 전에 테이블을 생성해야 하는 것처럼 문서를 추가하기 전에 인덱스를 생성해야 합니다.

Elasticsearch API를 사용하여 인덱스를 생성할 수 있습니다. 다음 예에서는 `name` 및 `address` 필드가 있는 `customers`라는 인덱스를 생성합니다.

```java
@Autowired
private ElasticsearchOperations operations;

@Test
public void testCreateIndex() {
    operations.createIndex(Customer.class);
}
```

# 인덱스에 데이터 추가

인덱스를 만든 후에 문서를 추가할 수 있습니다. 문서는 색인을 생성하려는 데이터가 포함된 JSON 객체입니다. 이 예에서는 고객 레코드를 인덱싱합니다. 각 고객 레코드에는 '이름'과 '주소'가 있습니다.

Elasticsearch API를 사용하여 문서를 색인화할 수 있습니다. 다음 예에서는 고객 레코드를 인덱싱합니다.

```java
@Autowired
private ElasticsearchOperations operations;

@Test
public void testIndex() {
    Customer customer = new Customer();
    customer.setName("John Smith");
    customer.setAddress("123 Main Street");

    operations.index(customer);
}
```

# 인덱스 검색

인덱스에 일부 데이터를 추가했으므로 이제 검색할 수 있습니다. Elasticsearch API를 사용하여 문서를 검색할 수 있습니다. 다음 예에서는 이름이 "John Smith"인 고객 레코드를 검색합니다.

```java
@Autowired
private ElasticsearchOperations operations;

@Test
public void testSearch() {
    QueryBuilder query = QueryBuilders.queryStringQuery("name:John Smith");
    SearchHits<Customer> customers = operations.search(query, Customer.class);

    assertEquals(1, customers.getTotalHits());
    assertEquals("John Smith", customers.getSearchHit(0).getContent().getName());
}
```

# 데이터 집계

문서 검색 외에도 색인에서 데이터를 집계할 수도 있습니다. Elasticsearch API를 사용하여 집계를 실행할 수 있습니다. 다음 예에서는 상태별로 고객 레코드를 집계합니다.

```java
@Autowired
private ElasticsearchOperations operations;

@Test
public void testAggregation() {
    QueryBuilder query = QueryBuilders.matchAllQuery();
    AggregationBuilder aggregation = AggregationBuilders.terms("by_state").field("address.state");
    SearchQuery searchQuery = new NativeSearchQueryBuilder()
            .withQuery(query)
            .withSearchType(SearchType.QUERY_THEN_FETCH)
            .withIndices("customers")
            .withTypes("customer")
            .addAggregation(aggregation)
            .build();

    Aggregations aggregations = operations.query(searchQuery, SearchResponse::getAggregations);
    StringTerms byStateAggregation = aggregations.get("by_state");
    assertEquals(2, byStateAggregation.getBuckets().size());
    assertEquals("CA", byStateAggregation.getBucketByKey("CA").getKeyAsString());
    assertEquals(1, byStateAggregation.getBucketByKey("CA").getDocCount());
    assertEquals("TX", byStateAggregation.getBucketByKey("TX").getKeyAsString());
    assertEquals(1, byStateAggregation.getBucketByKey("TX").getDocCount());
}
```

# 결론

이 게시물에서는 검색 및 분석을 위해 Spring Boot를 Elasticsearch와 통합하는 방법을 보여주었습니다. 먼저 Spring Boot 애플리케이션을 만들고 필요한 종속성을 추가했습니다. 그런 다음 Elasticsearch 인덱스를 생성하고 일부 데이터를 추가했습니다. 마지막으로 Elasticsearch API를 사용하여 인덱스에서 데이터를 검색하고 집계하는 Spring Boot 애플리케이션을 작성했습니다.