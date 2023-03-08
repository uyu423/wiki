---
title: RESTful API: HTTP로 웹 서비스 구축 소개
description: 
published: true
date: 2023-03-02T15:32:23.752Z
tags: 
editor: markdown
dateCreated: 2023-03-02T15:32:16.121Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [RESTful APIs: An Introduction to Building Web Services with HTTP***English** document is available*](/en/Knowledge-base/Network/restful-apis-an-introduction-to-building-web-services-with-http)
{.links-list}
RESTful API: HTTP로 웹 서비스 구축 소개

RESTful API는 웹 서비스 개발을 위해 개발자들 사이에서 점차 인기를 얻고 있습니다. REST는 Representational State Transfer의 약자로 가볍고 확장 가능하며 유지 관리가 가능한 웹 서비스를 만들기 위한 표준입니다. HTTP를 사용하면 RESTful API가 널리 사용되고 이해되기 때문에 개발자들 사이에서 인기 있는 선택이 됩니다. 이 기사에서는 HTTP를 사용하여 RESTful API를 구축하는 방법을 소개합니다.

## RESTful API란 무엇인가요?

RESTful API는 HTTP를 기반으로 웹 서비스를 구축하기 위한 아키텍처 스타일입니다. 해당 리소스에서 수행할 수 있는 작업보다는 웹 서비스에 의해 노출된 리소스에 중점을 둡니다. 리소스는 상태 비저장 방식으로 표시됩니다. 즉, 클라이언트에서 서버로의 각 요청에는 요청을 수행하는 데 필요한 모든 정보가 포함됩니다. 이는 확장성을 허용하고 API의 구현을 단순화합니다.

RESTful API는 다음 네 가지 기본 원칙을 기반으로 합니다.

1. **클라이언트-서버 아키텍처:** 클라이언트와 서버가 분리되어 있어 독립적으로 발전할 수 있습니다.

2. **상태 비저장:** 클라이언트와 서버는 서로에 대한 정보를 유지하지 않습니다. 각 요청은 독립적입니다.

3. **캐시 가능:** 응답은 캐시 가능 또는 캐시 불가능으로 표시되어야 합니다. 이를 통해 리소스를 보다 효율적으로 사용할 수 있습니다.

4. **균일한 인터페이스:** API에는 균일한 인터페이스가 있어야 합니다. 즉, URI를 사용하여 리소스를 식별해야 하며 이러한 리소스에 대한 작업에는 표준 HTTP 메서드를 사용해야 합니다.

## HTTP 메소드

HTTP 프로토콜은 여러 가지 방법을 지원하지만 RESTful API는 그 중 일부를 사용합니다. 가장 일반적으로 사용되는 방법은 다음과 같습니다.

1. **GET:** 서버에서 리소스를 가져옵니다.

2. **POST:** 서버에 새 리소스를 생성합니다.

3. **PUT:** 서버의 기존 리소스를 업데이트합니다.

4. **DELETE:** 서버에서 리소스를 삭제합니다.

5. **PATCH:** 서버의 기존 리소스를 부분적으로 업데이트합니다.

## HTTP 상태 코드

HTTP 상태 코드는 요청의 성공 또는 실패를 나타냅니다. RESTful API에서 가장 일반적으로 사용되는 상태 코드는 다음과 같습니다.

1. **200 OK:** 요청이 성공했습니다.

2. **201 생성됨:** 리소스가 성공적으로 생성되었습니다.

3. **204 No Content:** 요청에 성공했지만 응답 본문이 없습니다.

4. **400 잘못된 요청:** 요청 형식이 잘못되었거나 유효하지 않습니다.

5. **401 권한 없음:** 클라이언트가 요청을 수행할 권한이 없습니다.

6. **404 찾을 수 없음:** 요청한 리소스를 서버에서 찾을 수 없습니다.

7. **500 내부 서버 오류:** 요청을 처리하는 동안 서버에서 오류가 발생했습니다.

## 간단한 RESTful API 구축

HTTP로 RESTful API를 구축하는 방법을 설명하기 위해 책 관리를 위한 간단한 API를 생성해 보겠습니다. API에는 두 개의 엔드포인트가 있습니다. 하나는 책 목록을 검색하기 위한 것이고 다른 하나는 단일 책을 검색하기 위한 것입니다.

### 1단계: 데이터 모델 만들기

책에 대한 간단한 데이터 모델을 만드는 것으로 시작하겠습니다. `book.py`라는 파일을 만들고 다음 코드를 추가합니다.

```python
class Book:
    def __init__(self, id, title, author):
        self.id = id
        self.title = title
        self.author = author
```

이렇게 하면 `id`, `title` 및 `author`의 세 가지 속성이 있는 기본 `Book` 클래스가 생성됩니다.

### 2단계: API 엔드포인트 생성

다음으로 API에 대한 두 개의 끝점을 생성합니다. 하나는 책 목록을 검색하기 위한 것이고 다른 하나는 단일 책을 검색하기 위한 것입니다.

`api.py`라는 파일을 만들고 다음 코드를 추가합니다.

```python
from flask import Flask, jsonify
from book import Book

app = Flask(__name__)

books = [
    Book(1, 'The Hitchhiker\'s Guide to the Galaxy', 'Douglas Adams'),
    Book(2, '1984', 'George Orwell'),
    Book(3, 'The Catcher in the Rye', 'J.D. Salinger')
]

@app.route('/books', methods=['GET'])
def get_books():
    return jsonify({'books': [book.__dict__ for book in books]})

@app.route('/books/<int:book_id>', methods=['GET'])
def get_book(book_id):
    book = next((book for book in books if book.id == book_id), None)
    if book:
        return jsonify(book.__dict__)
    else:
        return jsonify({'error': 'Book not found'}), 404

if __name__ == '__main__':
    app.run()
```

이 코드는 Flask 애플리케이션을 설정하고 두 개의 끝점 `/books` 및 `/books/<int:book_id>`를 정의합니다. 첫 번째 끝점은 모든 책의 목록을 반환하고 두 번째 끝점은 해당 ID로 단일 책을 반환합니다.

### 3단계: API 테스트

API를 테스트하려면 `api.py` 파일을 실행하고 `http://localhost:5000/books`에 대한 브라우저를 열어 모든 책 또는 `http://localhost:5000/books/<book_id>`를 검색합니다. 한 권의 책을 되찾기 위해.

## 결론

RESTful API는 웹 서비스 구축을 위한 대중적인 선택이며 HTTP는 이러한 API 구축을 위한 기반입니다. REST의 원칙을 따르고 HTTP 프로토콜을 사용함으로써 개발자는 가볍고 확장 가능하며 유지 관리 가능한 웹 서비스를 만들 수 있습니다. 책 관리를 위한 간단한 RESTful API를 생성하여 HTTP를 사용하여 API를 구축하는 방법을 설명했습니다.

## 더 읽을거리

1. Roy Fielding의 [RESTful 웹 서비스](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)
2. [HTTP/1.1 사양](https://tools.ietf.org/html/rfc7231)
3. [플라스크 문서](https://flask.palletsprojects.com/)