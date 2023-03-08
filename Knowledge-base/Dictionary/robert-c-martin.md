---
title: Robert C. Martin
description: 
published: true
date: 2023-02-02T17:24:40.777Z
tags: 
editor: markdown
dateCreated: 2023-02-02T17:24:38.978Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Robert C. Martin***English** document is available*](/en/Knowledge-base/Dictionary/robert-c-martin)
{.links-list}


# 개요
Robert C. Martin(Uncle Bob이라고도 함)은 저명한 소프트웨어 엔지니어, 저자 및 연사입니다. 그는 SOLID 원칙과 같은 소프트웨어 설계 원칙에 대한 작업과 소프트웨어 엔지니어링 및 소프트웨어 장인 정신에 대한 저술로 잘 알려져 있습니다. 그는 애자일 소프트웨어 개발 사례를 강력하게 옹호하며 이 주제에 관한 여러 권의 책을 저술했습니다.

# 설명
Robert C. Martin은 SOLID 원칙과 같은 소프트웨어 설계 원칙에 대한 작업과 소프트웨어 엔지니어링 및 소프트웨어 장인 정신에 대한 저술로 잘 알려진 소프트웨어 엔지니어, 저자 및 연사입니다. 그는 애자일 소프트웨어 개발 사례를 강력하게 옹호하며 이 주제에 관한 여러 권의 책을 저술했습니다.

Martin은 성공적인 컨설팅 회사인 Object Mentor Inc.의 설립자이며 "Clean Code: A Handbook of Agile Software Craftsmanship" 및 "The Clean Coder: A Code of Conduct for Professional Programmers"를 비롯한 여러 책의 저자입니다. 그는 또한 유명한 소프트웨어 아키텍처 및 디자인 프레임워크인 Uncle Bob's Architecture의 창시자이기도 합니다.

Martin은 소프트웨어 장인 정신과 깨끗하고 유지 관리 가능한 코드 작성의 중요성을 강력하게 옹호합니다. 그는 컨퍼런스에서 자주 연설하며 소프트웨어 디자인, 소프트웨어 테스팅 및 소프트웨어 엔지니어링 모범 사례와 같은 주제에 대해 많은 강연을 했습니다.

# 역사
Robert C. Martin은 1952년 펜실베니아에서 태어나 1976년 매사추세츠 대학교에서 컴퓨터 공학 학위를 받고 졸업했습니다. 졸업 후 그는 소프트웨어 엔지니어로 일하기 시작했으며 이후 소프트웨어 업계에서 다양한 직책을 맡았습니다.

1980년대 후반에 Martin은 유지 관리 및 확장 가능한 소프트웨어를 만들기 위한 프레임워크를 제공하는 5가지 소프트웨어 설계 원칙 집합인 SOLID 원칙에 대한 작업을 시작했습니다. 1990년대 중반에 그는 소프트웨어 엔지니어링 및 소프트웨어 장인 정신에 대한 글을 쓰기 시작했으며 2000년에는 성공적인 컨설팅 회사인 Object Mentor Inc.를 설립했습니다.

그 이후로 Martin은 "Clean Code: A Handbook of Agile Software Craftsmanship" 및 "The Clean Coder: A Code of Conduct for Professional Programmers"를 비롯한 여러 권의 책을 저술했습니다. 그는 또한 유명한 소프트웨어 아키텍처 및 디자인 프레임워크인 Uncle Bob's Architecture의 창시자이기도 합니다.

# 특징
SOLID 원칙은 Robert C. Martin 작업의 초석이며 유지 관리 및 확장 가능한 소프트웨어를 만들기 위한 프레임워크를 제공하는 5가지 소프트웨어 설계 원칙 집합입니다. 이러한 원칙은 다음과 같습니다.

- 단일 책임 원칙: 클래스는 변경해야 하는 단 하나의 이유를 가져야 합니다.
- 개방-폐쇄 원칙: 소프트웨어 엔터티는 확장에는 열려 있어야 하지만 수정에는 닫혀 있어야 합니다.
- Liskov 대체 원칙: 파생 클래스는 기본 클래스를 대체할 수 있어야 합니다.
- 인터페이스 분리 원칙: 클라이언트가 사용하지 않는 메서드에 의존하도록 강요해서는 안 됩니다.
- 종속 역전 원칙: 구체화가 아닌 추상화에 의존합니다.

Martin은 또한 소프트웨어 장인 정신과 깨끗하고 유지 관리 가능한 코드 작성의 중요성을 강력하게 옹호합니다. 그는 소프트웨어 디자인, 소프트웨어 테스팅, 소프트웨어 엔지니어링 모범 사례와 같은 주제에 대해 여러 권의 책을 저술하고 많은 강연을 했습니다.

# 예
SOLID 원칙을 적용할 수 있는 방법의 예로 다음 코드를 고려하십시오.

```
class Database {
  public void save(String data) {
    // code to save data to the database
  }
 
  public void delete(String data) {
    // code to delete data from the database
  }
}
```

이 코드는 데이터 저장 및 삭제가 모두 동일한 클래스에서 처리되므로 단일 책임 원칙을 위반합니다. 원칙을 준수하려면 코드를 리팩토링하여 두 개의 별도 클래스(하나는 데이터 저장용, 다른 하나는 데이터 삭제용)를 만들어야 합니다.

# 장점과 단점
SOLID 원칙은 유지 관리 및 확장 가능한 소프트웨어를 만들기 위한 프레임워크를 제공하는 5가지 소프트웨어 설계 원칙 집합입니다. 이러한 원칙의 주요 이점은 각 클래스가 단일 책임을 가지며 확장에는 개방되지만 수정에는 폐쇄되므로 코드를 유지 관리하고 확장하기가 더 쉽다는 것입니다.

그러나 이러한 원칙에는 몇 가지 단점이 있습니다. 예를 들어 복잡한 시스템을 설계할 때 단일 책임 원칙을 준수하기 어려울 수 있으며 원칙을 준수하도록 코드를 리팩토링하는 데 더 많은 시간과 노력이 필요할 수 있습니다.

# 논란
소프트웨어 설계 원칙과 소프트웨어 장인 정신에 대한 Martin의 작업은 약간의 논란을 불러일으켰습니다. 일부에서는 SOLID 원칙이 너무 엄격하여 코드가 지나치게 복잡해질 수 있다고 주장했습니다. 다른 사람들은 소프트웨어 장인 정신에 대한 Martin의 초점이 시간이 많이 걸리고 항상 필요한 것은 아닌 "완벽한" 코드에 대한 초점으로 이어질 수 있다고 주장했습니다.

# 관련 기술
SOLID 원칙은 코드를 불필요하게 반복해서는 안 된다는 DRY(Don't Repeat Yourself) 원칙과 밀접한 관련이 있습니다. DRY 원칙은 종종 SOLID 원칙과 함께 사용되어 유지 관리 및 확장 가능한 코드를 생성합니다.

# 여담
Martin은 또한 민첩한 소프트웨어 개발 관행을 강력하게 옹호합니다. 그는 "Agile Software Development: Principles, Patterns, and Practices" 및 "The Agile Manifesto"를 포함하여 이 주제에 대해 여러 권의 책을 저술했습니다.

# 기타
소프트웨어 설계 및 애자일 소프트웨어 개발에 대한 그의 작업 외에도 Martin은 소프트웨어 테스팅의 강력한 옹호자이기도 합니다. 그는 "The Art of Software Testing" 및 "Test-Driven Development: By Example"을 포함하여 이 주제에 관한 여러 권의 책을 저술했습니다.