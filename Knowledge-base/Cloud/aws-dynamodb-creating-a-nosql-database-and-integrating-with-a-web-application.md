---
title: AWS DynamoDB: NoSQL 데이터베이스 생성 및 웹 애플리케이션과 통합
description: 
published: true
date: 2023-02-19T01:07:36.077Z
tags: 
editor: markdown
dateCreated: 2023-02-19T01:07:34.628Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [AWS DynamoDB: Creating a NoSQL Database and Integrating with a Web Application***English** document is available*](/en/Knowledge-base/Cloud/aws-dynamodb-creating-a-nosql-database-and-integrating-with-a-web-application)
{.links-list}


# DynamoDB NoSQL 데이터베이스

## 소개

DynamoDB는 Amazon에서 제공하는 빠르고 유연하며 확장 가능한 NoSQL 데이터베이스 서비스입니다. 키-값 저장소 또는 문서 데이터베이스로 사용할 수 있으며 다양한 응용 프로그램에 적합한 많은 기능이 있습니다.

이 기사에서는 DynamoDB 테이블을 생성하고 이를 웹 애플리케이션과 통합하는 방법을 살펴보겠습니다. 또한 DynamoDB의 몇 가지 주요 기능과 확장 가능하고 탄력적인 애플리케이션을 구축하는 데 어떻게 사용할 수 있는지 살펴보겠습니다.

## DynamoDB 테이블 생성

DynamoDB 테이블 생성은 간단한 과정입니다. 먼저 AWS Management Console에 로그인하고 서비스 목록에서 DynamoDB를 선택합니다.

![dynamodb-create-table-1](https://s3-us-west-2.amazonaws.com/itd-blog-assets/dynamodb-create-table-1.png)

다음 페이지에서 "테이블 만들기" 버튼을 클릭합니다.

![dynamodb-create-table-2](https://s3-us-west-2.amazonaws.com/itd-blog-assets/dynamodb-create-table-2.png)

테이블 이름을 입력하고 기본 키를 선택한 다음 "Provisioned" 처리량 모드를 선택합니다. 그런 다음 "만들기" 버튼을 클릭합니다.

![dynamodb-create-table-3](https://s3-us-west-2.amazonaws.com/itd-blog-assets/dynamodb-create-table-3.png)

다음 페이지에서 테이블에 대해 프로비저닝된 처리량을 구성할 수 있습니다. DynamoDB는 트래픽에 따라 자동으로 처리량을 늘리거나 줄이지만 필요한 경우 처리량을 수동으로 조정할 수도 있습니다.

![dynamodb-create-table-4](https://s3-us-west-2.amazonaws.com/itd-blog-assets/dynamodb-create-table-4.png)

프로비저닝된 처리량을 구성했으면 "만들기" 버튼을 클릭하여 테이블을 만듭니다.

## DynamoDB 테이블에 데이터 삽입

테이블이 생성되었으므로 테이블에 데이터를 삽입해 보겠습니다. DynamoDB는 테이블의 데이터 작업을 위한 간단한 API를 제공합니다. `putItem` 메서드를 사용하여 테이블에 새 항목을 삽입할 수 있습니다.

```javascript
var AWS = require('aws-sdk');

AWS.config.update({
  region: "us-west-2",
  endpoint: "http://localhost:8000"
});

var docClient = new AWS.DynamoDB.DocumentClient();

var table = "Movies";

var year = 2015;
var title = "The Big New Movie";

var params = {
    TableName:table,
    Item:{
        "year": year,
        "title": title,
        "info":{
            "plot": "Nothing happens at all.",
            "rating": 0
        }
    }
};

console.log("Adding a new item...");
docClient.put(params, function(err, data) {
    if (err) {
        console.error("Unable to add item. Error JSON:", JSON.stringify(err, null, 2));
    } else {
        console.log("Added item:", JSON.stringify(data, null, 2));
    }
});
```

이 코드는 기본 키 'year'와 정렬 키 'title'을 사용하여 새 항목을 테이블에 삽입합니다. `info` 속성에는 영화에 대한 정보 맵이 포함되어 있습니다.

## DynamoDB 테이블에서 데이터 검색

`getItem` 메서드를 사용하여 DynamoDB 테이블에서 항목을 검색할 수 있습니다. 다음 코드는 방금 삽입한 항목을 검색합니다.

```javascript
var params = {
    TableName:table,
    Key:{
        "year": year,
        "title": title
    }
};

docClient.get(params, function(err, data) {
    if (err) {
        console.error("Unable to read item. Error JSON:", JSON.stringify(err, null, 2));
    } else {
        console.log("GetItem succeeded:", JSON.stringify(data, null, 2));
    }
});
```

## DynamoDB 테이블의 데이터 업데이트

`updateItem` 메서드를 사용하여 DynamoDB 테이블의 기존 항목을 업데이트할 수 있습니다. 다음 코드는 앞에서 삽입한 항목에 대한 `info` 맵에 몇 가지 추가 정보를 추가합니다.

```javascript
var params = {
    TableName:table,
    Key:{
        "year": year,
        "title": title
    },
    UpdateExpression: "set info.rating = :r, info.plot=:p, info.actors=:a",
    ExpressionAttributeValues:{
        ":r":5.5,
        ":p":"Everything happens all at once.",
        ":a":["Larry", "Moe", "Curly"]
    },
    ReturnValues:"UPDATED_NEW"
};

console.log("Updating the item...");
docClient.update(params, function(err, data) {
    if (err) {
        console.error("Unable to update item. Error JSON:", JSON.stringify(err, null, 2));
    } else {
        console.log("UpdateItem succeeded:", JSON.stringify(data, null, 2));
    }
});
```

## DynamoDB 테이블에서 데이터 삭제

DynamoDB 테이블에서 기존 항목을 삭제하려면 `deleteItem` 메서드를 사용할 수 있습니다. 다음 코드는 앞에서 삽입한 항목을 삭제합니다.

```javascript
var params = {
    TableName:table,
    Key:{
        "year": year,
        "title": title
    }
};

console.log("Attempting a conditional delete...");
docClient.delete(params, function(err, data) {
    if (err) {
        console.error("Unable to delete item. Error JSON:", JSON.stringify(err, null, 2));
    } else {
        console.log("DeleteItem succeeded:", JSON.stringify(data, null, 2));
    }
});
```

## DynamoDB 스트림

DynamoDB Streams는 거의 실시간으로 DynamoDB 테이블 항목의 변경 사항을 추적할 수 있는 기능입니다. 스트림을 사용하여 데이터 변경에 응답하는 이벤트 기반 애플리케이션을 구축할 수 있습니다.

테이블에 대해 DynamoDB 스트림을 활성화하려면 테이블을 생성할 때 "Enable DynamoDB Streams" 확인란을 선택합니다.

![dynamodb-create-table-5](https://s3-us-west-2.amazonaws.com/itd-blog-assets/dynamodb-create-table-5.png)

테이블에 대해 DynamoDB 스트림이 활성화되면 테이블의 "개요" 탭을 클릭한 다음 "스트림" 탭을 클릭하여 스트림을 볼 수 있습니다.

![dynamodb-streams-1](https://s3-us-west-2.amazonaws.com/itd-blog-assets/dynamodb-streams-1.png)

DynamoDB 스트림은 레코드 스트림으로 구성되며 각 레코드는 테이블의 항목에 대한 변경 사항을 나타냅니다. [DynamoDB Streams 개발자 안내서](http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Streams.html)에서 DynamoDB Streams에 대해 자세히 알아볼 수 있습니다.

## DynamoDB 글로벌 테이블

DynamoDB 전역 테이블은 여러 AWS 리전에 걸쳐 DynamoDB 테이블을 복제할 수 있는 기능입니다. 이는 지역별 오류에 대한 복원력이 있거나 다른 지역의 사용자를 위해 데이터에 대한 짧은 대기 시간 액세스를 제공할 수 있는 애플리케이션을 구축하는 데 사용할 수 있습니다.

전역 테이블을 생성하려면 테이블을 생성할 때 "DynamoDB 전역 테이블 활성화" 확인란을 선택합니다.

![dynamodb-create-table-6](https://s3-us-west-2.amazonaws.com/itd-blog-assets/dynamodb-create-table-6.png)

다음 페이지에서 테이블을 복제할 AWS 리전을 선택할 수 있습니다.

![dynamodb-global-tables-1](https://s3-us-west-2.amazonaws.com/itd-blog-assets/dynamodb-global-tables-1.png)

테이블이 생성되면 테이블의 "개요" 탭을 클릭한 다음 "전역 테이블" 탭을 클릭하여 전역 테이블을 볼 수 있습니다.

![dynamodb-global-tables-2](https://s3-us-west-2.amazonaws.com/itd-blog-assets/dynamodb-global-tables-2.png)

DynamoDB 전역 테이블은 리전 간에 자동으로 데이터를 복제하므로 모든 리전의 테이블에서 데이터를 읽고 쓸 수 있습니다. [DynamoDB 전역 테이블 개발자 안내서](http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/GlobalTables.html)에서 DynamoDB 전역 테이블에 대해 자세히 알아볼 수 있습니다.

## 웹 애플리케이션과 DynamoDB 통합

DynamoDB 테이블을 생성하고 조작하는 방법을 살펴보았으니 이제 DynamoDB를 웹 애플리케이션과 통합하는 방법을 살펴보겠습니다. [AWS SDK for JavaScript](https://aws.amazon.com/sdk-for-javascript/)를 사용하여 Node.js 웹 애플리케이션에서 DynamoDB와 상호 작용합니다.

먼저 Node.js 패키지 관리자인 [npm](https://www.npmjs.com/)을 사용하여 SDK를 설치합니다.

```
npm install aws-sdk
```

다음으로 다음 코드를 포함하는 `dynamodb.js`라는 파일을 생성합니다. 이 코드는 SDK를 구성하고 DynamoDB 작업을 위한 메서드가 포함된 객체를 내보냅니다.

```javascript
var AWS = require('aws-sdk');

AWS.config.update({
  region: "us-west-2",
  endpoint: "http://localhost:8000"
});

var docClient = new AWS.DynamoDB.DocumentClient();

module.exports = {
  getMovies: function(year, title, callback) {
    var params = {
      TableName: "Movies",
      Key:{
        "year": year,
        "title": title
      }
    };

    docClient.get(params, function(err, data) {
      if (err) {
        console.error("Unable to read item. Error JSON:", JSON.stringify(err, null, 2));
      } else {
        callback(data);
      }
    });
  },
  addMovie: function(year, title, info, callback) {
    var params = {
      TableName: "Movies",
      Item:{
        "year": year,
        "title": title,
        "info": info
      }
    };

    docClient.put(params, function(err, data) {
      if (err) {
        console.error("Unable to add item. Error JSON:", JSON.stringify(err, null, 2));
      } else {
        callback();
      }
    });
  },
  updateMovie: function(year, title, info, callback) {
    var params = {
      TableName: "Movies",
      Key:{
        "year": year,
        "title": title
      },
      UpdateExpression: "set info.rating = :r, info.plot=:p, info.actors=:a",
      ExpressionAttributeValues:{
        ":r": info.rating,
        ":p": info.plot,
        ":a": info.actors
      },
      ReturnValues:"UPDATED_NEW"
    };

    docClient.update(params, function(err, data) {
      if (err) {
        console.error("Unable to update item. Error JSON:", JSON.stringify(err, null, 2));
      } else {
        callback();
      }
    });
  },
  deleteMovie: function(year, title, callback) {
    var params = {
      TableName: "Movies",
      Key:{
        "year": year,
        "title": title
      }
    };

    docClient.delete(params, function(err, data) {
      if (err) {
        console.error("Unable to delete item. Error JSON:", JSON.stringify(err, null, 2));
      } else {
        callback();
      }
    });
  }
}
```

이 코드는 로컬 DynamoDB 인스턴스에 연결하도록 SDK를 구성합니다. 그런 다음 DynamoDB 작업을 위한 메서드가 포함된 객체를 내보냅니다. 이러한 메서드는 DynamoDB 테이블에서 항목을 가져오고, 추가하고, 업데이트하고, 삭제하는 데 사용할 수 있습니다.

마지막으로 다음 코드를 포함하는 `server.js`라는 파일을 만듭니다. 이 코드는 [Express](https://expressjs.com/) 웹 프레임워크를 사용하여 간단한 웹 서버를 생성합니다. 또한 DynamoDB와 상호 작용하기 위해 `dynamodb.js` 파일에서 정의한 DynamoDB 메서드를 사용합니다.

```javascript
var express = require('express');
var app = express();
var bodyParser = require('body-parser');
var dynamodb = require('./dynamodb');

app.use(bodyParser.json());

app.get('/movies/:year/:title', function(req, res) {
  var year = req.params.year;
  var title = req.params.title;

  dynamodb.getMovies(year, title, function(data) {
    res.json(data);
  });
});

app.post('/movies', function(req, res) {
  var year = req.body.year;
  var title = req.body.title;
  var info = req.body.info;

  dynamodb.addMovie(year, title, info, function() {
    res.sendStatus(201);
  });
});

app.put('/movies/:year/:title', function(req, res) {
  var year = req.params.year;
  var title = req.params.title;
  var info = req.body.info;

  dynamodb.updateMovie(year, title, info, function() {
    res.sendStatus(200);
  });
});

app.delete('/movies/:year/:title', function(req, res) {
  var year = req.params.year;
  var title = req.params.title;

  dynamodb.deleteMovie(year, title, function() {
    res.sendStatus(200);
  });
});

app.listen(3000, function() {
  console.log('Movie API listening on port 3000!');
});
```

이 코드는 영화를 가져오고, 추가하고, 업데이트하고, 삭제하기 위한 경로를 정의합니다. 각 경로는 DynamoDB와 상호 작용하기 위해 `dynamodb.js` 파일에서 정의한 DynamoDB 메서드를 사용합니다.

## 결론

이 기사에서는 DynamoDB 테이블을 생성하고 이를 웹 애플리케이션과 통합하는 방법을 살펴보았습니다. 또한 DynamoDB Streams 및 DynamoDB Global Tables를 포함하여 DynamoDB의 일부 주요 기능을 사용하는 방법도 살펴보았습니다.

DynamoDB에 대해 자세히 알아보려면 [DynamoDB 개발자 안내서](http://docs.aws.amazon.com/amazondynamodb/latest/developerguide/)를 확인하십시오.