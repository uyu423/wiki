---
title: Object-Relational Mapping
description: 
published: true
date: 2023-03-13T01:32:43.336Z
tags: 
editor: markdown
dateCreated: 2023-03-13T01:32:43.336Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Object-Relational Mapping***English** document is available*](/en/Knowledge-base/Dictionary/object-relational-mapping)
{.links-list}

# 객체 관계형 매핑

## 개요
ORM(Object-Relational Mapping)은 개발자가 관계형 데이터베이스의 데이터를 객체 지향 프로그래밍 언어의 객체에 매핑할 수 있게 해주는 프로그래밍 기술입니다. 이 기술은 복잡한 SQL 쿼리를 작성할 필요가 없고 대신 개발자가 객체로 작업할 수 있도록 하여 데이터베이스 작업 프로세스를 단순화합니다.

## 설명
기존 프로그래밍에서 개발자는 데이터베이스와 상호 작용하기 위해 SQL 쿼리를 작성해야 했습니다. 이 프로세스는 특히 복잡한 쿼리로 작업할 때 시간이 많이 걸리고 오류가 발생하기 쉽습니다. ORM은 개발자가 SQL 쿼리 대신 개체로 작업할 수 있도록 하여 이 프로세스를 단순화합니다.

ORM은 데이터베이스 테이블을 개체 지향 프로그래밍 언어의 클래스에 매핑하여 작동합니다. 테이블의 각 행은 해당 클래스의 인스턴스에 매핑되고 테이블의 각 열은 클래스의 속성에 매핑됩니다. 이를 통해 개발자는 익숙한 프로그래밍 언어의 구문을 사용하여 보다 자연스러운 방식으로 데이터 작업을 수행할 수 있습니다.

ORM 프레임워크는 데이터베이스 작업을 쉽게 해주는 일련의 도구 및 라이브러리를 제공합니다. 이러한 프레임워크는 개발자가 데이터 쿼리, 삽입, 업데이트 및 삭제와 같은 일반적인 데이터베이스 작업을 수행할 수 있도록 하는 일련의 클래스 및 메서드를 제공합니다.

ORM 프레임워크는 또한 애플리케이션과 데이터베이스 사이에 추상화 계층을 제공합니다. 이는 개발자가 사용 중인 특정 데이터베이스와 독립적인 코드를 작성할 수 있음을 의미합니다. 이렇게 하면 데이터베이스 간을 쉽게 전환하거나 동일한 애플리케이션에서 여러 데이터베이스를 사용할 수도 있습니다.

## 역사
ORM의 개념은 최초의 객체 지향 데이터베이스가 개발된 1980년대로 거슬러 올라갑니다. 이러한 데이터베이스를 통해 개발자는 객체를 데이터베이스에 직접 저장할 수 있으므로 객체와 관계형 데이터베이스 간의 매핑이 필요하지 않습니다.

그러나 개체 지향 데이터베이스는 널리 채택되지 않았으며 관계형 데이터베이스는 여전히 지배적인 데이터베이스 기술로 남아 있었습니다. 1990년대에 개발자들은 관계형 데이터베이스를 객체에 매핑하는 기술을 개발하기 시작했으며, 이는 결국 ORM 프레임워크 개발로 이어졌습니다.

## 특징
ORM 프레임워크는 데이터베이스 작업을 보다 쉽게 해주는 여러 기능을 제공합니다.

- 데이터베이스 테이블을 클래스에 매핑
- 데이터베이스 열을 속성에 매핑
- SQL 쿼리 생성
- 쿼리 캐싱
- 거래 관리
- 연결 풀링
- 여러 데이터베이스 지원

## 예
다음은 ORM 프레임워크를 사용하여 데이터베이스에서 데이터를 검색하는 예입니다.

```python
from sqlalchemy import create_engine, Column, Integer, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import sessionmaker

engine = create_engine('postgresql://user:password@localhost/mydatabase')
Base = declarative_base()

class User(Base):
    __tablename__ = 'users'

    id = Column(Integer, primary_key=True)
    name = Column(String)
    age = Column(Integer)

Base.metadata.create_all(engine)

Session = sessionmaker(bind=engine)
session = Session()

users = session.query(User).filter(User.age > 18).all()

for user in users:
    print(user.name)
```

이 예에서는 SQLAlchemy ORM 프레임워크를 사용하여 데이터베이스에서 나이가 18세 이상인 모든 사용자를 검색합니다. 데이터베이스의 `users` 테이블에 매핑되는 `User` 클래스를 정의한 다음 `쿼리 ` 원하는 데이터를 검색하는 방법.

## 장점과 단점
ORM 프레임워크는 다음과 같은 많은 이점을 제공합니다.

- 데이터베이스 상호 작용 단순화
- 복잡한 SQL 쿼리의 필요성 감소
- 애플리케이션과 데이터베이스 간의 추상화 계층 제공
- 데이터베이스 간 전환이 더 쉬워집니다.

그러나 다음과 같은 몇 가지 단점도 있습니다.

- 복잡성 증가
- 잠재적인 성능 문제
- SQL 쿼리에 대한 제한된 제어

## 논란
ORM 프레임워크는 프로그래밍 커뮤니티에서 논란의 대상이었습니다. 일부 개발자는 애플리케이션에 불필요한 복잡성을 추가하고 성능 문제를 일으킬 수 있다고 주장합니다. 다른 사람들은 데이터베이스 상호 작용을 단순화하고 데이터베이스 작업을 더 쉽게 만든다고 주장합니다.

## 관련 기술
ORM 프레임워크는 종종 웹 프레임워크 및 데이터베이스 관리 시스템과 같은 다른 기술과 함께 사용됩니다. 인기 있는 ORM 프레임워크는 다음과 같습니다.

- SQLAlchemy(파이썬)
- 최대 절전 모드(자바)
- 엔티티 프레임워크(C# )

## 여담
ORM 프레임워크는 모든 데이터베이스 관련 문제에 대한 묘책이 아닙니다. 빈번한 데이터베이스 상호 작용이 필요하거나 여러 데이터베이스로 작업해야 하는 애플리케이션과 같이 이점이 단점보다 중요한 상황에서 가장 잘 사용됩니다.

## 기타
ORM 프레임워크는 데이터베이스 상호 작용을 단순화하고 데이터베이스 작업을 더 쉽게 만드는 강력한 도구입니다. 그러나 단점이 없는 것은 아니므로 개발자는 ORM 프레임워크가 애플리케이션에 적합한 선택인지 신중하게 고려해야 합니다.