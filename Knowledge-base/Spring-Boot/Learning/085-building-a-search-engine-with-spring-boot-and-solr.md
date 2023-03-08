---
title: 085: Spring Boot와 Solr로 검색 엔진 구축하기
description: 
published: true
date: 2023-02-05T15:33:30.480Z
tags: 
editor: markdown
dateCreated: 2023-02-05T15:33:24.897Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [085: Building a Search Engine with Spring Boot and Solr***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/085-building-a-search-engine-with-spring-boot-and-solr)
{.links-list}


# 085: Spring Boot와 Solr로 검색 엔진 구축하기

이 게시물에서는 [Spring Boot](https://spring.io/projects/spring-boot) 및 [Apache Solr](https://lucene.apache.org)를 사용하여 검색 엔진을 구축하는 방법을 보여줍니다. /solr/).

## 검색엔진이란?

검색 엔진은 사용자가 인터넷에서 정보를 찾을 수 있도록 하는 웹 기반 도구입니다. 검색 엔진은 알고리즘을 사용하여 웹 페이지를 크롤링하고 인덱싱하며 휴리스틱을 사용하여 관련 검색 결과를 사용자에게 제공합니다.

다양한 유형의 검색 엔진이 있지만 가장 인기 있는 검색 엔진은 Google, Yahoo 및 Bing과 같은 범용 검색 엔진입니다. 이러한 검색 엔진을 통해 사용자는 인터넷에서 무엇이든 검색할 수 있습니다.

## Apache Solr이란 무엇입니까?

[Apache Solr](https://lucene.apache.org/solr/)는 [Apache Lucene](https://lucene.apache.org/)을 기반으로 구축된 인기 있는 오픈 소스 엔터프라이즈 검색 플랫폼입니다. Solr는 Adobe, CNET 및 eBay를 비롯한 많은 대규모 조직에서 사용됩니다.

Solr은 색인 관리 및 검색을 위한 REST와 유사한 API를 제공하는 독립 실행형 검색 서버입니다. Solr은 확장성이 뛰어나며 분산 방식으로 배포할 수 있습니다.

## 솔라를 사용하는 이유?

Solr를 사용하는 데는 여러 가지 이유가 있지만 가장 인기 있는 이유는 다음과 같습니다.

- **Solr는 빠릅니다**: Solr는 대기 시간이 짧고 처리량이 높은 빠른 속도로 설계되었습니다.
- **Solr is scalable**: Solr은 확장성이 뛰어나고 분산 방식으로 배포할 수 있습니다.
- **Solr는 기능이 풍부합니다**: Solr는 전체 텍스트 검색, 패싯 검색 및 히트 강조 표시를 포함하여 즉시 사용할 수 있는 많은 기능을 제공합니다.

## 전제 조건

시작하기 전에 이 게시물을 따르기 위해 필요한 몇 가지 사항이 있습니다.

- **Java 8** 이상: [Oracle 웹 사이트](https://www.oracle.com/java/technologies/javase-downloads.html)에서 Java를 다운로드할 수 있습니다.
- **Maven**: [Apache Maven 웹사이트](https://maven.apache.org/install.html)에서 Maven을 설치할 수 있습니다.
- **Git**: [Git 웹사이트](https://git-scm.com/downloads)에서 Git을 설치할 수 있습니다.

## 시작하기

이 섹션에서는 검색 엔진을 시작하고 실행하는 데 필요한 단계를 안내합니다.

### 1단계: Spring Boot 프로젝트 생성

가장 먼저 해야 할 일은 새로운 Spring Boot 프로젝트를 만드는 것입니다. [Spring Initializr](https://start.spring.io/)를 사용하여 이를 수행할 수 있습니다.

다음 정보를 지정해야 합니다.

- **그룹**: 프로젝트의 그룹 ID입니다. 우리는 `com.example`을 사용할 것입니다.
- **아티팩트**: 프로젝트의 아티팩트 ID입니다. 우리는 `search-engine`을 사용할 것입니다.
- **이름**: 프로젝트의 이름입니다. 우리는 `검색 엔진`을 사용할 것입니다.
- **설명**: 프로젝트에 대한 설명입니다. Spring Boot와 Solr로 구축된 검색 엔진을 사용하겠습니다.
- **패키지 이름**: 프로젝트의 패키지 이름입니다. `com.example.search`를 사용하겠습니다.
- **패키징**: 프로젝트의 패키징 유형입니다. 우리는 `jar`를 사용할 것입니다.
- **Java 버전**: 프로젝트의 Java 버전입니다. `8`을 사용하겠습니다.
- **종속성**: 프로젝트의 종속성입니다. 다음 종속성을 추가해야 합니다.
  - `Web`: 이 종속성은 웹 개발에 대한 지원을 추가합니다.
  - `Solr`: 이 종속성은 Apache Solr에 대한 지원을 추가합니다.

모든 정보를 입력했으면 `프로젝트 생성` 버튼을 클릭하여 프로젝트를 다운로드할 수 있습니다.

### 2단계: Solr 구성

다음으로 Solr를 구성해야 합니다. 프로젝트의 `src/main/resources` 디렉토리에 `solr.xml`이라는 파일을 생성하여 이를 수행할 수 있습니다.

`solr.xml` 파일은 다음과 같아야 합니다.

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<solr>
  <solrcloud>
    <solrcloud>
      <zkHost>localhost:9983</zkHost>
    </solrcloud>
  </solrcloud>
  <shards>
    <shard>
      <name>shard1</name>
      <replicas>
        <replica>
          <name>replica1</name>
          <nodeName>node1</nodeName>
          <dataDir>data/shard1/replica1</dataDir>
        </replica>
      </replicas>
    </shard>
  </shards>
</solr>
```

`solr.xml` 파일에서 조정을 위해 [ZooKeeper](https://zookeeper.apache.org/)를 사용하도록 Solr를 구성했으며 단일 복제본으로 단일 샤드를 정의했습니다.

### 3단계: Solr Core 만들기

다음으로 Solr 코어를 생성해야 합니다. Solr 코어는 문서 모음을 포함하는 실행 중인 Solr 인스턴스입니다.

다음 명령을 실행하여 Solr 코어를 생성할 수 있습니다.

```
solr create -c <corename>
```

이 예에서는 `search-engine`이라는 이름을 사용합니다.

### 4단계: 스프링 부트 구성

이제 Solr 코어가 생성되었으므로 이를 사용하도록 Spring Boot를 구성해야 합니다. `application.properties` 파일에 다음 구성을 추가하여 이를 수행할 수 있습니다.

```properties
spring.data.solr.host=http://localhost:8983/solr/search-engine
```

구성에서 Solr 코어의 URL을 지정했습니다.

### 5단계: 문서 만들기

이제 Solr 코어가 구성되었으므로 여기에 문서를 추가할 수 있습니다. 문서는 Solr에서 인덱싱할 수 있는 정보 단위입니다.

`com.example.search.document` 패키지에 `SearchDocument`라는 새로운 Java 클래스를 생성하여 문서를 생성합니다. `SearchDocument` 클래스는 다음과 같아야 합니다.

```java
package com.example.search.document;

import org.apache.solr.client.solrj.beans.Field;
import org.springframework.data.annotation.Id;
import org.springframework.data.solr.core.mapping.SolrDocument;

@SolrDocument(solrCoreName = "search-engine")
public class SearchDocument {

    @Id
    @Field
    private String id;

    @Field
    private String title;

    @Field
    private String content;

    public String getId() {
        return id;
    }

    public void setId(String id) {
        this.id = id;
    }

    public String getTitle() {
        return title;
    }

    public void setTitle(String title) {
        this.title = title;
    }

    public String getContent() {
        return content;
    }

    public void setContent(String content) {
        this.content = content;
    }
}
```

`SearchDocument` 클래스에서 `@SolrDocument` 주석으로 클래스에 주석을 추가하여 Solr 문서임을 나타냅니다. 또한 `id`, `title` 및 `content` 필드에 `@Field` 주석을 추가하여 Solr에 의해 인덱싱되어야 함을 나타냅니다.

### 6단계: 서비스 만들기

이제 문서가 생성되었으므로 문서를 인덱싱할 수 있는 서비스를 생성해야 합니다. `com.example.search.service` 패키지에 `SearchService`라는 새로운 Java 인터페이스를 생성합니다. `SearchService` 인터페이스는 다음과 같아야 합니다.

```java
package com.example.search.service;

import com.example.search.document.SearchDocument;

public interface SearchService {

    void indexDocument(SearchDocument document);

}
```

`SearchService` 인터페이스에서 `SearchDocument` 개체를 허용하고 색인화하는 `indexDocument`라는 단일 메서드를 정의했습니다.

다음으로 `SearchServiceImpl`이라는 `SearchService` 인터페이스의 구현을 만듭니다. `SearchServiceImpl` 클래스는 다음과 같아야 합니다.

```java
package com.example.search.service;

import com.example.search.document.SearchDocument;
import org.apache.solr.client.solrj.SolrClient;
import org.apache.solr.client.solrj.SolrServerException;
import org.apache.solr.common.SolrInputDocument;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import java.io.IOException;

@Service
public class SearchServiceImpl implements SearchService {

    @Autowired
    private SolrClient solrClient;

    @Override
    public void indexDocument(SearchDocument document) {
        SolrInputDocument solrInputDocument = new SolrInputDocument();
        solrInputDocument.addField("id", document.getId());
        solrInputDocument.addField("title", document.getTitle());
        solrInputDocument.addField("content", document.getContent());

        try {
            solrClient.add(solrInputDocument);
            solrClient.commit();
        } catch (SolrServerException | IOException e) {
            // log error
        }
    }
}
```

`SearchServiceImpl` 클래스에서 `SolrClient` 개체를 삽입했습니다. `SolrClient` 개체는 Solr 서버와 상호 작용하는 데 사용됩니다.

또한 `indexDocument` 메서드도 구현했습니다. `indexDocument` 메서드에서 `SolrInputDocument` 개체를 만들고 `SearchDocument` 개체의 필드를 여기에 추가했습니다.

마지막으로 `SolrInputDocument`를 `SolrClient`에 추가하고 변경 사항을 커밋했습니다.

### 7단계: 컨트롤러 만들기

이제 서비스가 생성되었으므로 문서를 인덱싱할 수 있는 컨트롤러를 생성해야 합니다. `com.example.search.controller` 패키지에 `SearchController`라는 새로운 Java 클래스를 생성합니다. `SearchController` 클래스는 다음과 같아야 합니다.

```java
package com.example.search.controller;

import com.example.search.document.SearchDocument;
import com.example.search.service.SearchService;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/search")
public class SearchController {

    @Autowired
    private SearchService searchService;

    @PostMapping
    public void indexDocument(@RequestBody SearchDocument document) {
        searchService.indexDocument(document);
    }

}
```

`SearchController` 클래스에서 `SearchService` 개체를 삽입했습니다. 또한 `SearchDocument` 개체를 허용하는 `indexDocument`라는 주석이 달린 `@PostMapping` 메서드도 만들었습니다.

`indexDocument` 메서드에서 `SearchService` 객체의 `indexDocument` 메서드를 호출하여 문서를 인덱싱했습니다.

### 8단계: 애플리케이션 빌드 및 실행

이제 애플리케이션이 생성되었으므로 빌드하고 실행할 수 있습니다. 다음 명령을 실행하여 이를 수행할 수 있습니다.

```
mvn spring-boot:run
```

애플리케이션이 실행되면 요청 본문에 `SearchDocument` 개체가 있는 `/search` 끝점에 POST 요청을 보내 문서를 색인화할 수 있습니다.

## 결론

이번 포스트에서는 Spring Boot와 Solr를 사용하여 검색 엔진을 구축하는 방법을 보여드렸습니다. 또한 Solr를 구성하는 방법과 문서를 인덱싱하는 방법도 보여 주었습니다.