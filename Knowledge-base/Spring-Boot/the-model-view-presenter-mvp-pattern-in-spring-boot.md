---
title: Spring Boot의 MVP(Model-View-Presenter) 패턴
description: 
published: true
date: 2023-01-31T11:23:20.490Z
tags: 
editor: markdown
dateCreated: 2023-01-31T11:23:18.891Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [The Model-View-Presenter (MVP) Pattern in Spring Boot***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-model-view-presenter-mvp-pattern-in-spring-boot)
{.links-list}


  MVP 패턴은 사용자 인터페이스를 만드는 데 사용되는 MVC 패턴의 파생물입니다. 이것은 애플리케이션의 관심사를 모델, 뷰 및 프리젠터의 세 부분으로 분리하기 때문에 웹 애플리케이션에서 널리 사용되는 선택입니다. 이러한 관심사의 분리는 코드를 보다 유지 관리하기 쉽고 테스트하기 쉽게 만듭니다.

MVP 패턴은 모델, 뷰 및 컨트롤러도 있다는 점에서 MVC 패턴과 유사합니다. 그러나 MVP 패턴에는 몇 가지 중요한 차이점이 있습니다. 첫째, MVP 패턴은 뷰와 모델 사이에 직접적인 연결이 없습니다. 대신 발표자는 둘 사이의 중재자 역할을 합니다. 이를 통해 뷰와 모델이 서로 완전히 독립적일 수 있습니다. 둘째, MVP 패턴은 발표자를 더 강조합니다. 발표자는 모든 사용자 입력을 처리하고 그에 따라 보기를 업데이트할 책임이 있습니다.

MVP 패턴을 사용하면 많은 이점이 있습니다. 첫째, 코드를 단위 테스트하기가 더 쉬워집니다. 둘째, 기본 코드를 변경하지 않고도 사용자 인터페이스를 쉽게 변경할 수 있습니다. 셋째, 다른 목적으로 코드를 재사용하기가 더 쉬워집니다.

다음 Spring Boot 프로젝트에서 MVP 패턴을 사용하는 데 관심이 있다면 염두에 두어야 할 몇 가지 사항이 있습니다. 먼저 각 보기에 대해 별도의 프레젠터 클래스를 생성해야 합니다. 둘째, 프리젠터를 뷰에 주입해야 합니다. 셋째, 뷰를 프리젠터에 바인딩해야 합니다. 넷째, 프리젠터를 모델에 연결해야 합니다. 마지막으로 프리젠터에 뷰를 등록해야 합니다.

모든 작업을 완료하면 Spring Boot 프로젝트에서 MVP 패턴을 사용할 준비가 된 것입니다.