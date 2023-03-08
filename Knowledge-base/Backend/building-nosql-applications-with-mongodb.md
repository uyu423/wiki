---
title: MongoDB로 NoSQL 애플리케이션 구축
description: 
published: true
date: 2023-02-01T22:06:04.254Z
tags: 
editor: markdown
dateCreated: 2023-02-01T22:06:01.503Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building NoSQL Applications with MongoDB***English** document is available*](/en/Knowledge-base/Backend/building-nosql-applications-with-mongodb)
{.links-list}


# MongoDB로 NoSQL 애플리케이션 구축

## 소개

MongoDB는 10gen에서 개발 및 지원하는 오픈 소스 문서 지향 데이터베이스 시스템입니다. NoSQL 데이터베이스 시스템 제품군의 일부입니다. NoSQL 데이터베이스는 높은 트래픽과 데이터 볼륨을 처리할 수 있으므로 웹 애플리케이션에 점점 더 많이 사용되고 있습니다.

MongoDB는 JSON과 유사한 문서 형식을 사용하며 인덱스 기반 검색 기능이 있습니다. 또한 풍부한 쿼리 언어가 있습니다. 이러한 기능 덕분에 MongoDB는 NoSQL 애플리케이션을 구축하려는 개발자에게 매력적인 옵션입니다.

## 몽고DB 설정

이 섹션에서는 MongoDB 설정의 기본 사항을 다룹니다. 로컬 머신에 MongoDB를 설치하고 간단한 데이터베이스를 생성합니다.

### 몽고DB 설치하기

MongoDB는 10gen 웹 사이트(http://www.10gen.com/)에서 다운로드할 수 있습니다. Windows, OS X 및 Linux용 버전이 있습니다. MongoDB가 다운로드되면 운영 체제의 지침에 따라 설치합니다.

### 데이터베이스 생성

우리는 책에 대한 정보를 저장하기 위해 간단한 데이터베이스를 만들 것입니다. 이 데이터베이스에는 두 개의 컬렉션이 있습니다. 하나는 책용이고 다른 하나는 저자용입니다.

먼저 MongoDB 서버를 시작해야 합니다. Windows의 경우 `mongod` 실행 파일을 실행하여 이 작업을 수행할 수 있습니다. OS X 및 Linux의 경우 터미널에서 `mongod` 명령을 실행하여 MongoDB를 시작할 수 있습니다.

MongoDB 서버가 실행되면 `mongo` 클라이언트를 사용하여 연결할 수 있습니다. 그러면 명령을 입력할 수 있는 `mongod>` 프롬프트가 표시됩니다.

먼저 `books` 컬렉션을 만들어야 합니다. `db.createCollection()` 메서드를 사용하여 이 작업을 수행할 수 있습니다.

    ```자바스크립트
    db.createCollection("책")
    ```

그런 다음 `db.books.insert()` 메서드를 사용하여 일부 데이터를 컬렉션에 삽입할 수 있습니다. 각 책에 대한 문서를 삽입합니다.

    ```자바스크립트
    db.책.삽입({
        "제목": "모비 딕",
        "저자": "허먼 멜빌",
        "연도": 1851
    })

    db.책.삽입({
        "제목": "호밀밭의 파수꾼",
        "저자": "J.D. 샐린저",
        "연도": 1951
    })

    db.책.삽입({
        "title": "앵무새 죽이기",
        "저자": "하퍼 리",
        "연도": 1960
    })
    ```

그런 다음 `authors` 컬렉션을 만들고 동일한 메서드를 사용하여 데이터를 여기에 삽입할 수 있습니다.

    ```자바스크립트
    db.createCollection("작성자")

    db.작성자.삽입({
        "이름": "허먼 멜빌",
        "태어난": 1819,
        "사망": 1891,
        "책": ["모비 딕"]
    })

    db.작성자.삽입({
        "이름": "J.D. 샐린저",
        "태어난": 1919,
        "사망": 2010,
        "책": ["호밀밭의 파수꾼"]
    })

    db.작성자.삽입({
        "이름": "하퍼 리",
        "태어난": 1926,
        "사망": 2016,
        "책": ["앵무새 죽이기"]
    })
    ```

그런 다음 `db.collection.find()` 메서드를 사용하여 컬렉션의 데이터를 쿼리할 수 있습니다. 예를 들어 J.D. Salinger가 쓴 모든 책을 찾으려면 다음 쿼리를 사용합니다.

    ```자바스크립트
    db.books.find({"저자": "J.D. 샐린저"})
    ```

## NoSQL 애플리케이션 구축

이 섹션에서는 책에 대한 정보를 표시하는 간단한 웹 애플리케이션을 빌드합니다. 이전 섹션에서 생성한 MongoDB 데이터베이스를 사용합니다.

Node.js 플랫폼을 사용하여 애플리케이션을 빌드합니다. Node.js는 웹 애플리케이션 구축에 널리 사용되는 플랫폼입니다. 가볍고 응용 프로그램에 기능을 추가하는 데 사용할 수 있는 모듈의 대규모 에코 시스템이 있습니다.

Express.js 웹 애플리케이션 프레임워크를 사용합니다. Express.js는 Node.js로 웹 애플리케이션을 구축하는 데 널리 사용되는 선택입니다. 사용하기 쉽고 많은 기능이 있습니다.

Jade 템플릿 엔진을 사용하여 웹 페이지용 HTML을 생성합니다. Jade는 사용하기 쉽고 깨끗한 HTML을 생성하는 인기 있는 템플릿 엔진입니다.

Mongoose.js 모듈을 사용하여 MongoDB 데이터베이스와 인터페이스할 것입니다. Mongoose.js는 Node.js에서 MongoDB로 쉽게 작업할 수 있게 해주는 인기 있는 모듈입니다.

### 종속성 설치

먼저 사용할 모듈을 설치해야 합니다. Node.js에 포함된 `npm` 패키지 관리자를 사용하여 이 작업을 수행할 수 있습니다. 명령줄에서 모듈을 사용할 수 있도록 전역적으로 모듈을 설치합니다.

명령줄에서 다음 명령을 사용하여 필요한 모듈을 설치할 수 있습니다.

    npm 설치 -g 익스프레스
    npm 설치 -g 옥
    npm install -g 몽구스

### 애플리케이션 만들기

이제 애플리케이션용 파일을 생성합니다. 먼저 애플리케이션의 루트 디렉토리에 `app.js`라는 파일을 생성합니다. 이 파일에는 웹 애플리케이션용 코드가 포함됩니다.

먼저 설치한 모듈을 요청하고 애플리케이션의 기본 구조를 설정합니다.

    ```자바스크립트
    var 익스프레스 = 요구("익스프레스");
    var jade = require("옥");
    var 몽구스 = require("몽구스");

    var 앱 = 익스프레스();

    app.set("뷰 엔진", "제이드");
    app.set("뷰", __dirname + "/뷰");

    app.use(express.static(__dirname + "/public"));
    ```

그런 다음 경로를 정의합니다. 우리는 두 개의 경로를 만들 것입니다. 하나는 홈 페이지용이고 다른 하나는 도서 세부 정보 페이지용입니다.

홈페이지 경로의 경우 `books` 컬렉션을 쿼리하고 결과를 표시하는 템플릿을 렌더링합니다.

    ```자바스크립트
    app.get("/", function(req, res) {
        db.books.find(function(err, books) {
            경우 (오류) {
                // 오류 처리
            } 또 다른 {
                res.render("색인", { 책: 책 });
            }
        });
    });
    ```

책 세부 정보 페이지의 경우 `books` 및 `authors` 컬렉션을 쿼리하고 결과를 표시하는 템플릿을 렌더링합니다.

    ```자바스크립트
    app.get("/book/:id", function(req, res) {
        db.books.findById(req.params.id, function(err, book) {
            경우 (오류) {
                // 오류 처리
            } 또 다른 {
                db.authors.findById(book.author, function(err, author) {
                    경우 (오류) {
                        // 오류 처리
                    } 또 다른 {
                        res.render("책", { 책: 책, 저자: 저자 });
                    }
                });
            }
        });
    });
    ```

그런 다음 템플릿을 정의합니다. 우리는 두 개의 템플릿을 만들 것입니다. 하나는 홈 페이지용이고 다른 하나는 책 세부 정보 페이지용입니다.

홈페이지 템플릿의 경우 `books` 배열을 반복하고 각 책에 대한 정보를 표시합니다.

    ```옥
    레이아웃 확장

    콘텐츠 차단
        h1= 제목

        울
            책 속의 각 책
                리
                    a(href="/book/# {book._id}")= 책.제목
    ```

책 세부 정보 페이지 템플릿의 경우 책과 저자에 대한 정보를 표시합니다.

    ```옥
    레이아웃 확장

    콘텐츠 차단
        h1= 책.제목

        피
            | 작성자
            a(href="/author/# {author._id}")= 저자.이름

        p= 책.년
    ```

그런 다음 `views` 디렉토리에 `layout.jade`라는 파일을 생성합니다. 이 파일에는 애플리케이션의 레이아웃 템플릿이 포함됩니다.

    ```옥
    독타입 HTML
    HTML
        머리
            제목 = 제목
            링크(rel='stylesheet', href='/stylesheets/style.css')
        신체
            콘텐츠 차단
    ```

그런 다음 `public/stylesheets` 디렉토리에 `style.css`라는 파일을 생성합니다. 이 파일에는 애플리케이션의 CSS가 포함됩니다.

    ```css
    신체 {
        font-family: 산세리프;
    }

    h1 {
        글꼴 두께: 정상;
    }
    ```

그런 다음 애플리케이션의 루트 디렉토리에 `package.json`이라는 파일을 생성합니다. 이 파일에는 애플리케이션에 대한 종속성이 포함됩니다.

    ```자바스크립트
    {
        "이름": "도서 앱",
        "버전": "0.0.1",
        "종속성": {
            "익스프레스": "3.x",
            "옥": "1.x",
            "몽구스": "3.x"
        }
    }
    ```

그런 다음 애플리케이션의 루트 디렉토리에 `Procfile`이라는 파일을 생성합니다. 이 파일은 Heroku에게 애플리케이션을 시작하는 방법을 알려줍니다.

    ```
    웹: 노드 app.js
    ```

### 데이터베이스에 연결

이제 MongoDB 데이터베이스에 연결하기 위해 `app.js` 파일을 수정합니다. `mongoose.connect()` 메서드를 사용하여 데이터베이스에 연결합니다. 경로에서 사용할 수 있도록 `db`라는 변수에 연결을 저장합니다.

    ```자바스크립트
    var db = mongoose.connect("mongodb://localhost/book-app");
    ```

그런 다음 모델을 정의합니다. 우리는 두 가지 모델을 만들 것입니다. 하나는 책용이고 다른 하나는 저자용입니다.

책 모델의 경우 데이터베이스에 저장하려는 필드를 정의합니다.

    ```자바스크립트
    var bookSchema = 몽구스.스키마({
        제목: 문자열,
        작성자: 몽구스.Schema.Types.ObjectId,
        연도: 숫자
    });

    var Book = mongoose.model("도서", bookSchema);
    ```

작성자 모델의 경우 데이터베이스에 저장하려는 필드를 정의합니다.

    ```자바스크립트
    var authorSchema = 몽구스.스키마({
        이름: 문자열,
        출생: 번호,
        사망: 번호,
        책: [mongoose.Schema.Types.ObjectId]
    });

    var Author = mongoose.model("저자", authorSchema);
    ```

그런 다음 모델을 사용하도록 경로를 수정합니다.

홈페이지 경로의 경우 `books` 컬렉션을 쿼리하고 결과를 표시하는 템플릿을 렌더링합니다.

    ```자바스크립트
    app.get("/", function(req, res) {
        Book.find(function(err, books) {
            경우 (오류) {
                // 오류 처리
            } 또 다른 {
                res.render("색인", { 책: 책 });
            }
        });
    });
    ```

책 세부 정보 페이지의 경우 `books` 및 `authors` 컬렉션을 쿼리하고 결과를 표시하는 템플릿을 렌더링합니다.

    ```자바스크립트
    app.get("/book/:id", function(req, res) {
        Book.findById(req.params.id, function(err, book) {
            경우 (오류) {
                // 오류 처리
            } 또 다른 {
                Author.findById(book.author, function(err, author) {
                    경우 (오류) {
                        // 오류 처리
                    } 또 다른 {
                        res.render("책", { 책: 책, 저자: 저자 });
                    }
                });
            }
        });
    });
    ```

## 애플리케이션 배포

이 섹션에서는 응용 프로그램을 Heroku에 배포합니다. Heroku는 웹 애플리케이션을 쉽게 배포하고 확장할 수 있게 해주는 인기 있는 PaaS(Platform as a Service)입니다.

먼저 Heroku 계정(https://signup.heroku.com/)을 만들어야 합니다. 계정이 생성되면 Heroku Toolbelt(https://toolbelt.heroku.com/)를 설치해야 합니다. Heroku Toolbelt는 Heroku 애플리케이션을 관리하는 데 사용할 수 있는 명령줄 인터페이스(CLI)입니다.

Heroku Toolbelt가 설치되면 `heroku login` 명령을 사용하여 계정에 로그인할 수 있습니다. 이메일 주소와 비밀번호를 입력하라는 메시지가 표시됩니다.

그런 다음 `heroku create` 명령을 사용하여 Heroku 애플리케이션을 만들 수 있습니다. 이렇게 하면 새 애플리케이션이 생성되고 고유한 이름이 지정됩니다. 선택적으로 `--app` 플래그를 사용하여 애플리케이션의 이름을 지정할 수 있습니다.

    heroku create --app my-app-name

그런 다음 `git push heroku master` 명령을 사용하여 응용 프로그램을 Heroku에 배포할 수 있습니다. 이렇게 하면 Git 리포지토리의 `master` 브랜치에서 `heroku` 원격으로 코드가 푸시됩니다.

    git push 헤로쿠 마스터

그런 다음 `heroku open` 명령을 사용하여 웹 브라우저에서 애플리케이션을 열 수 있습니다. 그러면 새 탭에서 애플리케이션의 홈 페이지가 열립니다.

    헤로쿠 오픈

## 결론

이 기사에서는 MongoDB로 NoSQL 애플리케이션을 구축하는 기본 사항을 다뤘습니다. MongoDB 설치 방법, 데이터베이스 생성 방법, NoSQL 애플리케이션 구축 방법 및 애플리케이션을 Heroku에 배포하는 방법을 다루었습니다.

NoSQL 데이터베이스는 웹 애플리케이션에서 점점 더 대중화되고 있습니다. MongoDB는 문서 지향 데이터 모델, 인덱스 기반 검색 기능 및 풍부한 쿼리 언어로 인해 NoSQL 애플리케이션에 널리 사용됩니다.

Node.js는 웹 애플리케이션 구축에 널리 사용되는 플랫폼입니다. 가볍고 모듈의 큰 생태계를 가지고 있습니다. Express.js는 Node.js용으로 널리 사용되는 웹 애플리케이션 프레임워크입니다. Jade는 사용하기 쉽고 깨끗한 HTML을 생성하는 인기 있는 템플릿 엔진입니다. Mongoose.js는 Node.js에서 MongoDB로 쉽게 작업할 수 있게 해주는 인기 있는 모듈입니다.

Heroku는 웹 애플리케이션을 쉽게 배포하고 확장할 수 있게 해주는 인기 있는 PaaS(Platform as a Service)입니다.