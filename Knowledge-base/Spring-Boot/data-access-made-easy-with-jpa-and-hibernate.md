---
title: JPA 및 Hibernate로 데이터 액세스가 쉬워졌습니다.
description: 
published: true
date: 2023-01-30T01:05:56.823Z
tags: 
editor: markdown
dateCreated: 2023-01-30T01:05:56.823Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Data Access Made Easy with JPA and Hibernate***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/data-access-made-easy-with-jpa-and-hibernate)
{.links-list}


# JPA 및 Hibernate로 데이터 액세스가 쉬워졌습니다.

엔티티 클래스는 JPA(Java Persistence API)의 핵심입니다. 데이터를 클래스로 표현함으로써 JPA를 사용하면 개체 지향 방식으로 관계형 데이터베이스에 데이터를 저장할 수 있습니다. 또한 Java 개체를 사용하여 데이터를 쉽게 쿼리하고 수정할 수 있습니다.

JPA(Java Persistence API)는 Java 애플리케이션에서 데이터베이스에 액세스하는 표준 방법을 제공하는 Java EE 사양입니다. JPA는 JDBC(Java DatabaseConnectivity) API를 기반으로 구축되어 SQL을 사용하여 데이터베이스에 액세스할 수 있습니다.

JPA는 두 가지 유형의 엔티티 bean을 제공합니다.

- JPA 엔터티: JPA 엔터티는 데이터베이스 테이블에 매핑되는 Java 클래스입니다. JPA 엔티티는 JPA 엔티티 관리자가 관리합니다.

- Hibernate 엔터티: Hibernate 엔터티는 데이터베이스 테이블에 매핑되는 Java 클래스입니다. Hibernate 엔터티는 Hibernate 세션에 의해 관리됩니다.

이 기사에서는 JPA 엔티티에 중점을 둘 것입니다.

관계형 데이터베이스에 데이터를 저장하려면 데이터베이스 스키마를 정의해야 합니다. 스키마는 데이터베이스의 구조를 정의합니다. 테이블, 각 테이블의 열 및 테이블 간의 관계를 지정합니다.

JPA를 사용하면 주석을 사용하여 스키마를 정의할 수 있습니다. 주석은 Java 클래스에 추가할 수 있는 메타데이터 조각입니다. 주석을 사용하면 스키마를 정의하기 위해 SQL 코드를 작성하지 않아도 됩니다.

JPA에서는 @Entity 주석을 사용하여 Java 클래스를 엔티티 빈으로 표시합니다. @Table 주석을 사용하여 엔티티 빈을 데이터베이스 테이블에 매핑합니다.

@Column 주석을 사용하여 필드를 데이터베이스 테이블의 열에 매핑합니다. 기본적으로 열 이름은 필드 이름과 동일합니다. 그러나 @Column 주석을 사용하여 다른 열 이름을 지정할 수 있습니다.

@Id 주석을 사용하여 엔티티 빈의 기본 키로 필드를 표시합니다. 기본 키는 엔티티 bean을 고유하게 식별하는 데 사용됩니다.

@GeneratedValue 주석을 사용하여 필드 값을 생성합니다. 이는 기본 키인 필드에 유용합니다. 기본적으로 생성된 값은 일련의 숫자입니다. 그러나 @GeneratedValue 주석을 사용하여 다른 값 생성 전략을 지정할 수 있습니다.

@ManyToOne 주석을 사용하여 일대다 관계를 매핑할 수 있습니다. 이 주석은 관계의 다측면을 나타내는 필드에서 사용됩니다.

@OneToMany 주석을 사용하여 일대다 관계를 매핑할 수 있습니다. 이 주석은 관계의 한쪽을 나타내는 필드에서 사용됩니다.

JPA에서는 EntityManager를 사용하여 엔티티 bean을 관리합니다. EntityManager는 엔티티 bean을 생성, 업데이트 및 삭제하는 데 사용됩니다.

EntityManagerFactory를 사용하여 EntityManager를 얻습니다. EntityManagerFactory는 엔티티 관리자를 구성하는 데 사용됩니다.

Persistence 클래스를 사용하여 EntityManagerFactory를 얻습니다. Persistence 클래스는 persistence.xml 파일을 로드하는 데 사용됩니다. persistence.xml 파일은 EntityManagerFactory를 구성하는 데 사용됩니다.

JPA에서는 Query 인터페이스를 사용하여 쿼리를 생성합니다. 쿼리 인터페이스는 쿼리를 실행하는 데 사용됩니다.

TypedQuery 인터페이스를 사용하여 유형이 지정된 쿼리를 생성합니다. 유형이 지정된 쿼리는 특정 유형의 엔터티 빈을 반환하는 쿼리입니다.

CriteriaQuery 인터페이스를 사용하여 기준 쿼리를 생성합니다. 조건 쿼리는 조건을 지정하여 만드는 쿼리입니다.

QueryBuilder 인터페이스를 사용하여 쿼리 빌더를 생성합니다. 쿼리 빌더는 쿼리를 동적으로 생성하는 데 사용됩니다.

JPA에서는 EntityTransaction을 사용하여 트랜잭션을 관리합니다. EntityTransaction은 트랜잭션을 시작, 커밋 및 롤백하는 데 사용됩니다.

JPA에서는 Query setParameter 메서드를 사용하여 쿼리의 매개변수를 설정합니다. Query setFirstResult 및 setMaxResults 메서드를 사용하여 쿼리의 페이지 매김을 설정합니다.

Query setHint 메서드를 사용하여 쿼리에 대한 힌트를 설정합니다. 힌트는 JPA 공급자에게 쿼리 실행 방법에 대한 힌트를 제공하는 데 사용됩니다.

Query setFlushMode 메서드를 사용하여 쿼리의 플러시 모드를 설정합니다. 플러시 모드는 엔티티 bean에 대한 변경 사항이 데이터베이스에 플러시되는 시기를 제어하는 데 사용됩니다.

Query setLockMode 메서드를 사용하여 쿼리의 잠금 모드를 설정합니다. 잠금 모드는 쿼리가 데이터베이스를 잠그는 방법을 제어하는 데 사용됩니다.

Query getResultList 메서드를 사용하여 쿼리를 실행하고 결과를 목록으로 가져옵니다.

Query getSingleResult 메서드를 사용하여 쿼리를 실행하고 결과를 단일 결과로 가져옵니다.

Query getResultStream 메서드를 사용하여 쿼리를 실행하고 결과를 스트림으로 가져옵니다.

Query getResultList 및 getSingleResult 메서드를 사용하여 조건 쿼리를 실행합니다.

Query getResultStream 메서드를 사용하여 기준 쿼리를 실행하고 결과를 스트림으로 가져옵니다.

JPA에서는 EntityManager 플러시 메서드를 사용하여 엔티티 빈에 대한 변경 사항을 데이터베이스에 플러시합니다.

EntityManager clear 메서드를 사용하여 EntityManager를 지웁니다.

EntityManager 닫기 메서드를 사용하여 EntityManager를 닫습니다.

EntityManager에서 엔티티 빈을 분리하기 위해 EntityManager 분리 메소드를 사용합니다.

EntityManager에 Entity Bean이 연결되어 있는지 확인하기 위해 EntityManager contains 메서드를 사용합니다.

EntityManager getReference 메소드를 사용하여 엔티티 bean에 대한 참조를 가져옵니다.

EntityManager 병합 방법을 사용하여 엔티티 빈을 EntityManager와 병합합니다.

JPA에서는 @ PersistenceContext 주석을 사용하여 EntityManager를 주입합니다.

@PersistenceUnit 주석을 사용하여 EntityManagerFactory를 주입합니다.

JPA에서는 @TransactionAttribute 주석을 사용하여 메서드를 트랜잭션으로 표시합니다.

@Transactional 어노테이션을 사용하여 클래스를 트랜잭션으로 표시합니다.

JPA에서는 @TransactionManagement 주석을 사용하여 트랜잭션 관리 유형을 지정합니다.

@PrePersist 및 @PostPersist 주석을 사용하여 엔터티 bean이 지속되기 전과 후에 호출할 메서드를 표시합니다.

@PreRemove 및 @PostRemove 주석을 사용하여 엔티티 bean이 제거되기 전과 후에 호출할 메서드를 표시합니다.

@PreUpdate 및 @PostUpdate 주석을 사용하여 엔터티 bean이 업데이트되기 전과 후에 호출할 메서드를 표시합니다.

@PostLoad 주석을 사용하여 엔터티 빈이 로드된 후 호출할 메서드를 표시합니다.

JPA에서는 @IdClass 주석을 사용하여 복합 기본 키를 매핑합니다.

임베디드 기본 키를 매핑하기 위해 @EmbeddedId 주석을 사용합니다.

JPA에서는 @AttributeOverrides 주석을 사용하여 여러 필드를 동일한 열에 매핑합니다.

@AssociationOverrides 주석을 사용하여 여러 필드를 동일한 관계에 매핑합니다.

@ColumnTransformer 주석을 사용하여 필드를 SQL 함수로 계산되는 열에 매핑합니다.

JPA에서는 @ElementCollection 주석을 사용하여 기본 유형 컬렉션을 매핑합니다.

@CollectionTable 어노테이션을 사용하여 엔티티 bean 콜렉션을 맵핑합니다.

JPA에서는 @JoinColumn 주석을 사용하여 외래 키 열을 매핑합니다.

@JoinColumns 주석을 사용하여 여러 외래 키 열을 매핑합니다.

@MapKeyColumn 주석을 사용하여 지도의 키 열을 매핑합니다.

JPA에서는 @MappedSuperclass 주석을 사용하여 클래스를 매핑된 슈퍼클래스로 표시합니다.

@Inheritance 주석을 사용하여 상속 전략을 지정합니다.

JPA에서는 @DiscriminatorValue 주석을 사용하여 엔티티 빈의 판별자 값을 지정합니다.

@DiscriminatorColumn 주석을 사용하여 판별자 열을 지정합니다.

JPA에서는 @Version 주석을 사용하여 버전 필드를 매핑합니다.

CascadeType.ALL 주석은 모든 작업을 계단식으로 배열하는 데 사용됩니다.

CascadeType.PERSIST 주석은 지속 작업을 계단식으로 연결하는 데 사용됩니다.

CascadeType.MERGE 주석은 병합 작업을 계단식으로 배열하는 데 사용됩니다.

CascadeType.REMOVE 주석은 제거 작업을 계단식으로 만드는 데 사용됩니다.

CascadeType.REFRESH 주석은 새로 고침 작업을 계단식으로 만드는 데 사용됩니다.

JPA에서는 @NamedQueries 주석을 사용하여 명명된 쿼리를 지정합니다.

명명된 쿼리를 지정하기 위해 @NamedQuery 주석을 사용합니다.

JPA에서는 @NamedNativeQueries 주석을 사용하여 명명된 네이티브 쿼리를 지정합니다.

@NamedNativeQuery 주석을 사용하여 명명된 네이티브 쿼리를 지정합니다.

JPA에서는 @SqlResultSetMapping 주석을 사용하여 네이티브 SQL 쿼리의 결과를 엔터티 빈 또는 POJO에 매핑합니다.

명명된 저장 프로시저 쿼리를 지정하기 위해 @NamedStoredProcedureQueries 주석을 사용합니다.

명명된 저장 프로시저 쿼리를 지정하기 위해 @NamedStoredProcedureQuery 주석을 사용합니다.

JPA에서는 @QueryHints 주석을 사용하여 쿼리 힌트를 지정합니다.

@Lock 주석을 사용하여 잠금 모드를 지정합니다.

JPA에서는 @QueryRedirections 주석을 사용하여 쿼리 리디렉션을 지정합니다.

@FetchProfile 주석은 가져오기 프로필을 지정하는 데 사용됩니다.

JPA에서는 @FetchProfiles 주석을 사용하여 가져오기 프로필을 지정합니다.

@FetchProfile.Subclass 주석은 하위 클래스에 대한 가져오기 프로필을 지정하는 데 사용됩니다.

JPA에서는 CriteriaUpdate 인터페이스를 사용하여 기준 업데이트 쿼리를 생성합니다.

CriteriaDelete 인터페이스를 사용하여 기준 삭제 쿼리를 생성합니다.

JPA에서는 NativeQuery 인터페이스를 사용하여 네이티브 SQL 쿼리를 생성합니다.

NamedNativeQuery 인터페이스는 명명된 네이티브 SQL 쿼리를 만드는 데 사용됩니다.

JPA에서는 Query 인터페이스를 사용하여 쿼리를 생성합니다.

TypedQuery 인터페이스는 유형이 지정된 쿼리를 만드는 데 사용됩니다.

NamedQuery 인터페이스는 명명된 쿼리를 만드는 데 사용됩니다.

QueryHint 인터페이스는 쿼리 힌트를 지정하는 데 사용됩니다.

JPA에서는 QueryRedirection 인터페이스를 사용하여 쿼리 리디렉션을 지정합니다.

EntityManager 인터페이스는 엔티티 bean을 관리하는 데 사용됩니다.

EntityManagerFactory 인터페이스는 EntityManager를 얻는 데 사용됩니다.

Persistence 클래스는 EntityManagerFactory를 얻는 데 사용됩니다.

EntityTransaction 인터페이스는 트랜잭션을 관리하는 데 사용됩니다.

쿼리 인터페이스는 쿼리를 만들고 실행하는 데 사용됩니다.

CriteriaQuery 인터페이스는 기준 쿼리를 생성하는 데 사용됩니다.

QueryBuilder 인터페이스는 쿼리 빌더를 생성하는 데 사용됩니다.

FetchProfile 인터페이스는 가져오기 프로필을 지정하는 데 사용됩니다.