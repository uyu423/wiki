---
title: Node.js 및 Elasticsearch: 검색 및 분석 실습 가이드
description: 
published: true
date: 2023-02-15T12:56:04.105Z
tags: 
editor: markdown
dateCreated: 2023-02-15T12:56:02.175Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Node.js and Elasticsearch: A Hands-On Guide to Search and Analytics***English** document is available*](/en/Knowledge-base/Nodejs/node-js-and-elasticsearch-a-hands-on-guide-to-search-and-analytics)
{.links-list}


# Node.js 및 Elasticsearch: 검색 및 분석 실습 가이드

이 기사에서는 Node.js와 Elasticsearch를 사용하여 강력한 검색 및 분석 솔루션을 구축하는 방법을 살펴보겠습니다. Node.js 개발 환경을 설정하는 것으로 시작한 다음 Elasticsearch 서버 및 클라이언트 라이브러리를 설치합니다.

다음으로 일부 데이터를 Elasticsearch로 인덱싱하고 Elasticsearch Query DSL을 사용하여 쿼리하는 간단한 Node.js 애플리케이션을 생성합니다. 또한 강력한 데이터 분석 쿼리를 구축하기 위해 Elasticsearch 집계를 사용하는 방법도 살펴보겠습니다.

마지막으로 Heroku를 사용하여 Node.js 및 Elasticsearch 애플리케이션을 클라우드에 배포하는 방법을 살펴보겠습니다.

## Node.js 개발 환경 설정

Node.js 애플리케이션을 위한 개발 환경을 설정하는 것부터 시작하겠습니다. Node.js와 몇 가지 다른 도구를 설치해야 합니다.

### Node.js 설치하기

먼저 Node.js를 설치해야 합니다. Homebrew와 같은 패키지 관리자를 사용하여 이 작업을 수행할 수 있습니다.

```shell
brew install node
```

또는 [Node.js 웹사이트](https://nodejs.org/en/)에서 Node.js 바이너리를 다운로드하여 설치할 수 있습니다.

Node.js가 설치되면 다음 명령을 실행하여 작동하는지 확인할 수 있습니다.

```shell
node -v
```

이렇게 하면 Node.js 버전 번호가 콘솔에 출력됩니다.

### 다른 도구 설치

Node.js 외에도 몇 가지 다른 도구를 설치해야 합니다.

- 코드 편집기. [Visual Studio Code](https://code.visualstudio.com/)를 추천합니다.
- [Git](https://git-scm.com/), 버전 관리용.
- 컨테이너에서 Elasticsearch 서버를 실행하기 위한 [Docker](https://www.docker.com/).

## Elasticsearch 서버 설치

첫 번째 단계는 Elasticsearch 서버를 설치하는 것입니다. Docker를 사용하여 이 작업을 수행할 수 있습니다.

```shell
docker run -d -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" --name es elasticsearch:7.5.0
```

이렇게 하면 포트 9200에서 Elasticsearch 서버를 실행하는 Docker 컨테이너가 시작됩니다. `/_cluster/health` 엔드포인트에 HTTP 요청을 전송하여 서버가 실행 중인지 확인할 수 있습니다.

```shell
curl -X GET "localhost:9200/_cluster/health?pretty"
```

이것은 Elasticsearch 클러스터의 상태와 함께 JSON 응답을 반환해야 합니다.

```json
{
  "cluster_name" : "docker-cluster",
  "status" : "green",
  "timed_out" : false,
  "number_of_nodes" : 1,
  "number_of_data_nodes" : 1,
  "active_primary_shards" : 0,
  "active_shards" : 0,
  "relocating_shards" : 0,
  "initializing_shards" : 0,
  "unassigned_shards" : 0,
  "delayed_unassigned_shards" : 0,
  "number_of_pending_tasks" : 0,
  "number_of_in_flight_fetch" : 0,
  "task_max_waiting_in_queue_millis" : 0,
  "active_shards_percent_as_number" : 100
}
```

[http://localhost:9200](http://localhost:9200)에서 Elasticsearch 서버 웹 인터페이스에 액세스할 수도 있습니다.

## Elasticsearch Node.js 클라이언트 설치

이제 Elasticsearch 서버가 가동되어 실행 중이므로 Elasticsearch Node.js 클라이언트를 설치할 수 있습니다. [npm](https://www.npmjs.com/) 패키지 관리자를 사용하여 이 작업을 수행할 수 있습니다.

```shell
npm install elasticsearch
```

그러면 `elasticsearch` Node.js 모듈이 설치되고 `package.json` 파일의 `dependencies` 섹션에 추가됩니다.

## Node.js 애플리케이션 만들기

이제 모든 것이 설정되었으므로 Node.js 애플리케이션 생성을 시작할 수 있습니다. 애플리케이션 종속성을 관리하기 위해 `package.json` 파일을 생성하여 시작하겠습니다.

```shell
npm init
```

그러면 이름 및 버전과 같은 응용 프로그램에 대한 일부 정보를 묻는 메시지가 표시됩니다. 'Enter'를 눌러 기본값을 수락할 수 있습니다.

다음으로 프로젝트 루트 디렉토리에 다음 내용으로 `index.js`라는 파일을 생성합니다.

```javascript
const { Client } = require('elasticsearch');

const client = new Client({
  host: 'localhost:9200'
});

(async () => {
  // Index some data into Elasticsearch
  await client.index({
    index: 'my-index',
    type: 'my-type',
    id: '1',
    body: {
      title: 'My first document',
      body: 'This is my first document'
    }
  });
  
  // Query the data using the Elasticsearch Query DSL
  const result = await client.search({
    index: 'my-index',
    type: 'my-type',
    body: {
      query: {
        match: {
          body: 'first'
        }
      }
    }
  });
  
  console.log(result.hits.hits);
})();
```

이 코드는 Elasticsearch 클라이언트 개체를 생성하고 이를 사용하여 일부 데이터를 Elasticsearch로 인덱싱하고 Elasticsearch Query DSL을 사용하여 쿼리합니다.

## 데이터를 Elasticsearch로 인덱싱

데이터를 Elasticsearch로 인덱싱하는 코드를 자세히 살펴보겠습니다. 먼저 다음 속성을 사용하여 `인덱스` 개체를 만듭니다.

- `인덱스`: 인덱스의 이름입니다.
- `유형`: 문서의 유형입니다.
- `id`: 문서의 ID입니다.
- `body`: 문서 본문입니다.

그런 다음 `index` 메서드를 사용하여 문서를 Elasticsearch로 인덱싱합니다.

```javascript
await client.index({
  index: 'my-index',
  type: 'my-type',
  id: '1',
  body: {
    title: 'My first document',
    body: 'This is my first document'
  }
});
```

이렇게 하면 문서가 `my-type` 유형과 ID `1`인 `my-index` 인덱스로 인덱싱됩니다.

## Elasticsearch Query DSL을 사용하여 데이터 쿼리

일부 데이터를 Elasticsearch로 인덱싱했으므로 이제 데이터를 쿼리하는 방법을 살펴보겠습니다. Elasticsearch는 Query DSL이라는 강력한 쿼리 언어를 제공합니다.

Query DSL을 사용하여 인덱스에서 특정 문서를 검색하는 데 사용할 수 있는 복잡한 쿼리를 작성할 수 있습니다.

위의 코드 예제에서는 `body` 필드에 `first`라는 용어가 포함된 모든 문서를 찾기 위해 `match` 쿼리를 사용합니다.

```javascript
const result = await client.search({
  index: 'my-index',
  type: 'my-type',
  body: {
    query: {
      match: {
        body: 'first'
      }
    }
  }
});
```

이 쿼리는 이전에 인덱싱한 문서와 일치하고 `result` 개체에 반환합니다.

## 클라우드에 배포

이제 작동하는 Node.js 및 Elasticsearch 애플리케이션이 있으므로 클라우드에 배포해 보겠습니다. 이를 위해 [Heroku](https://www.heroku.com/)를 사용합니다.

먼저 프로젝트 루트 디렉토리에 다음 내용을 포함하는 ` Procfile `을 생성해야 합니다.

```
web: node index.js
```

이 파일은 Heroku에게 애플리케이션 시작 방법을 알려줍니다.

다음으로 프로젝트 루트 디렉토리에 다음 내용으로 `.env` 파일을 생성해야 합니다.

```
ES_HOST=localhost
ES_PORT=9200
```

이 파일에는 애플리케이션에서 사용할 환경 변수가 포함되어 있습니다.

마지막으로 프로젝트 루트 디렉토리에 다음 내용으로 ` heroku.yml ` 파일을 생성해야 합니다.

```yaml
build:
  docker:
    web: Dockerfile
```

이 파일은 Heroku에게 Docker를 사용하여 애플리케이션을 빌드하도록 지시합니다.

이러한 파일이 생성되면 다음 명령을 사용하여 응용 프로그램을 Heroku에 배포할 수 있습니다.

```shell
heroku create
git push heroku master
```

이렇게 하면 새 Heroku 애플리케이션이 생성되고 여기에 코드가 배포됩니다.

## 결론

이 기사에서는 Node.js와 Elasticsearch를 사용하여 강력한 검색 및 분석 솔루션을 구축하는 방법을 살펴보았습니다. 개발 환경을 설정하고 Elasticsearch 서버를 설치하는 것으로 시작했습니다.

다음으로 데이터를 Elasticsearch로 인덱싱하고 Elasticsearch Query DSL을 사용하여 쿼리하는 간단한 Node.js 애플리케이션을 만들었습니다. 또한 강력한 데이터 분석 쿼리를 구축하기 위해 Elasticsearch 집계를 사용하는 방법도 살펴보았습니다.

마지막으로 Heroku를 사용하여 Node.js 및 Elasticsearch 애플리케이션을 클라우드에 배포하는 방법을 살펴보았습니다.

## 외부 리소스

- [Node.js](https://nodejs.org/)
- [Elasticsearch](https://www.elastic.co/products/elasticsearch)
- [도커](https://www.docker.com/)
- [헤로쿠](https://www.heroku.com/)