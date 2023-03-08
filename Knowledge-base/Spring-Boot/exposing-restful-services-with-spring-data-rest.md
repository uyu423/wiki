---
title: Spring 데이터 REST로 RESTful 서비스 노출
description: 
published: true
date: 2023-02-17T18:02:25.992Z
tags: 
editor: markdown
dateCreated: 2023-01-30T09:16:41.495Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Exposing RESTful Services with Spring Data REST***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/exposing-restful-services-with-spring-data-rest)
{.links-list}


REST는 확장 가능하고 유지 관리가 가능하며 빠른 웹 서비스를 구축하기 위한 아키텍처 스타일입니다. REST 아키텍처 스타일을 준수하는 웹 서비스 또는 RESTful 웹 서비스는 사용 및 이해하기 쉬운 클라이언트 및 서버용 일관된 인터페이스를 제공합니다.

REST 아키텍처 스타일을 사용하는 이점 중 하나는 웹 서비스의 데이터와 기능을 클라이언트가 액세스하고 사용할 수 있는 리소스로 쉽게 노출할 수 있다는 것입니다. 이를 통해 클라이언트는 서비스 구현 방법을 몰라도 웹 서비스의 데이터 및 기능에 액세스하고 사용할 수 있습니다.

Spring Data REST는 Spring Data 라이브러리로 생성된 데이터 저장소에 대한 RESTful 인터페이스를 쉽게 노출할 수 있게 해주는 라이브러리입니다. Spring Data REST는 Spring Data의 기능을 사용하고 Spring Data 리포지토리에 저장된 데이터에 액세스하는 데 사용할 수 있는 RESTful 인터페이스의 기본 구현을 추가합니다.

이 게시물에서는 Spring Data REST를 사용하여 데이터 저장소에 대한 RESTful 인터페이스를 노출하는 방법을 살펴보겠습니다. Spring Data REST를 사용하여 RESTful 인터페이스에 사용자 정의 기능을 추가하는 방법도 살펴보겠습니다.

Spring Data로 생성된 데이터 저장소는 Spring Data REST를 사용하여 RESTful 리소스로 쉽게 노출될 수 있습니다. 리포지토리 인터페이스에 @RepositoryRestResource 주석을 추가하기만 하면 됩니다.

@RepositoryRestResource 주석은 리포지토리가 REST 리소스로 노출되어야 함을 나타내는 데 사용됩니다. 주석은 리포지토리의 인터페이스와 구현 클래스 모두에서 사용할 수 있습니다.

주석이 인터페이스에서 사용되면 인터페이스가 REST 리소스로 노출됩니다. 주석이 구현 클래스에서 사용되면 인터페이스와 구현 클래스가 모두 REST 리소스로 노출됩니다.

@RepositoryRestResource 주석에는 리포지토리가 REST 리소스로 노출되는 방식을 구성하는 데 사용할 수 있는 여러 속성이 있습니다.

path 속성은 REST 리소스의 경로를 지정하는 데 사용됩니다. 기본값은 엔터티의 대문자가 아닌 복수형 이름입니다.

CollectionResourceRel 속성은 상위 자원에 대한 콜렉션 자원의 관계를 지정하는 데 사용됩니다. 기본값은 CollectionResourceRel.ITEM입니다.

Exported 속성은 리포지토리를 REST 리소스로 내보내야 하는지 여부를 지정하는 데 사용됩니다. 기본값은 참입니다.

maxPageSize 특성은 결과의 단일 페이지에 반환될 수 있는 최대 항목 수를 지정하는 데 사용됩니다. 기본값은 Integer.MAX_VALUE입니다.

pageSize 속성은 단일 결과 페이지에 반환되어야 하는 기본 항목 수를 지정하는 데 사용됩니다. 기본값은 20입니다.

PagedResourcesAssembler 속성은 findAll() 메서드의 결과를 페이징 리소스 객체로 어셈블하는 데 사용해야 하는 페이징 리소스 어셈블러를 지정하는 데 사용됩니다.

Projection 특성은 리포지토리에서 데이터를 노출하는 데 사용해야 하는 프로젝션을 지정하는 데 사용됩니다. 기본값은 null입니다.

Rel 속성은 리소스의 관계를 지정하는 데 사용됩니다. 기본값은 자체입니다.

ResourceDescription 특성은 리소스에 대한 설명을 지정하는 데 사용됩니다. 기본값은 null입니다.

ResourceRelation 속성은 자원의 자원 관계를 지정하는 데 사용됩니다. 기본값은 ResourceRelation.SELF입니다.

Sort 특성은 findAll() 메서드의 결과를 정렬하는 데 사용해야 하는 정렬을 지정하는 데 사용됩니다. 기본값은 null입니다.

@RepositoryRestResource(경로 = "사람", collectionResourceRel = "사람", 내보낸 = true, maxPageSize = 50, pageSize = 20)
공개 인터페이스 PersonRepository 확장 CrudRepository<Person, Long> {

}
위의 예에서 PersonRepository는 경로 /people에서 REST 리소스로 노출됩니다. 컬렉션 리소스의 이름은 people로 지정되고 내보내집니다. 단일 결과 페이지에 반환할 수 있는 최대 항목 수는 50개입니다. 단일 결과 페이지에 반환해야 하는 기본 항목 수는 20개입니다.

Spring Data REST를 사용하면 RESTful 인터페이스에 사용자 정의 기능을 추가할 수도 있습니다. 이는 사용자 정의 컨트롤러를 생성하고 애플리케이션 컨텍스트에 추가하여 수행됩니다.

 @RestController
 @RequestMapping("/사람")
 공개 클래스 PersonController {

     @Autowired
     개인 PersonRepository 저장소;

     @RequestMapping(메서드 = RequestMethod.GET)
     공개 목록 <사람> findAll() {
         return repository.findAll();
     }

     @RequestMapping(방법 = RequestMethod.POST)
     공개 사람 추가(@RequestBody 사람 사람) {
         return repository.save(사람);
     }

     @RequestMapping(방법 = RequestMethod.PUT)
     public 사람 업데이트(@RequestBody 사람 사람) {
         return repository.save(사람);
     }

     @RequestMapping(값 = "/{id}", 메서드 = RequestMethod.DELETE)
     공개 무효 삭제(@PathVariable 긴 ID) {
         저장소.삭제(id);
     }
 }
위의 예에서는 모든 사람을 찾고, 사람을 추가하고, 사람을 업데이트하고, 사람을 삭제하는 방법을 제공하는 사용자 지정 컨트롤러가 만들어집니다. 이러한 메서드는 /people 경로에 대한 HTTP GET, POST, PUT 및 DELETE 요청을 만드는 클라이언트에서 호출할 수 있습니다.

REST 리소스로 노출되는 리포지토리에 사용자 지정 메서드를 추가할 수도 있습니다. 이러한 메서드는 리소스 경로에 대한 HTTP GET 요청을 만드는 클라이언트에서 호출할 수 있습니다.

@RepositoryRestResource
공개 인터페이스 PersonRepository 확장 CrudRepository<Person, Long> {

    @RestResource(경로 = "findByName")
    public List<Person> findByName(@Param("이름") 문자열 이름);
}
위의 예에서 이름으로 사람을 찾는 데 사용할 수 있는 사용자 지정 메서드가 PersonRepository에 추가되었습니다. 이 메소드는 /people/findByName?name=<name> 경로에 HTTP GET 요청을 하는 클라이언트에 의해 호출될 수 있습니다.

 Spring Data REST는 데이터 저장소를 REST 리소스로 쉽게 노출할 수 있게 해주는 라이브러리입니다. Spring Data REST를 사용하면 REST 인터페이스에 사용자 정의 기능을 추가할 수 있습니다. 이 게시물에서는 Spring Data REST를 사용하여 데이터 리포지토리를 REST 리소스로 노출하는 방법을 살펴보았습니다.