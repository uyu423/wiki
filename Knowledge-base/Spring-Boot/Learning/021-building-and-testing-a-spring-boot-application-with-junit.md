---
title: 021: Junit으로 Spring Boot 애플리케이션 빌드 및 테스트
description: 
published: true
date: 2023-02-03T13:34:18.814Z
tags: 
editor: markdown
dateCreated: 2023-02-03T13:34:17.066Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [021: Building and testing a Spring Boot application with Junit***English** document is available*](/en/Knowledge-base/Spring-Boot/Learning/021-building-and-testing-a-spring-boot-application-with-junit)
{.links-list}


# 021: Junit으로 Spring Boot 애플리케이션 빌드 및 테스트

Junit은 Java 애플리케이션용으로 널리 사용되는 테스트 프레임워크입니다. Spring Boot는 마이크로 서비스 및 웹 애플리케이션을 만드는 데 사용되는 Java 기반 프레임워크입니다. 이 게시물에서는 Junit을 사용하여 Spring Boot 애플리케이션을 빌드하고 테스트하는 방법을 보여줍니다.

이 자습서에서는 다음 도구를 사용합니다.

- 자바 8
- 메이븐 3.3.9
- 이클립스 Neon.3
- Junit 4.12

## 스프링 부트 애플리케이션 만들기

Spring Boot 애플리케이션을 만드는 것부터 시작하겠습니다. 이 자습서에서는 Spring Initializr 웹 사이트를 사용하여 프로젝트를 생성합니다.

Spring Initializr 웹 사이트(https://start.spring.io/)로 이동하여 다음 정보를 입력합니다.

- 그룹: com.example
- 아티팩트: junit-튜토리얼
- 이름: junit-튜토리얼
- 설명: Junit 튜토리얼 데모 프로젝트
- 패키지 이름: com.example.junit.tutorial
- 포장: 항아리
- 자바 버전: 1.8
- 다음 종속성 선택: Web, JPA, H2, Lombok

프로젝트 생성을 클릭하여 프로젝트를 다운로드합니다.

zip 파일을 추출하고 Maven 프로젝트로 Eclipse에 가져옵니다.

## 테스트 케이스 작성

이제 프로젝트가 설정되었으므로 테스트 사례 작성을 시작할 수 있습니다. 다음 시나리오를 테스트할 것입니다.

- 사용자 이름이 "johndoe"이고 암호가 "password"인 사용자
- 사용자가 로그인을 시도하는 경우
- 그러면 사용자가 성공적으로 로그인할 수 있어야 합니다.

com.example.junit.tutorial.service 패키지에 새 Java 클래스를 만들고 이름을 LoginServiceTest.java로 지정합니다. 클래스에 다음 코드를 추가합니다.

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class LoginServiceTest {

    @Autowired
    private LoginService loginService;

    @Test
    public void testLogin() {
        // given
        String username = "johndoe";
        String password = "password";

        // when
        boolean result = loginService.login(username, password);

        // then
        assertTrue(result);
    }
}
```

위의 코드에서 @RunWith 및 @SpringBootTest 주석을 사용하여 테스트 사례를 실행하고 있습니다. 또한 login() 메서드를 테스트할 수 있도록 LoginService를 테스트 사례에 주입하고 있습니다.

login() 메서드는 사용자 이름과 암호를 사용하고 로그인 성공 여부를 나타내는 부울 값을 반환합니다. 테스트 사례에서는 사용자 이름과 비밀번호 "johndoe" 및 "password"를 전달합니다. 그런 다음 결과가 참이라고 어설션합니다. 이는 로그인이 성공했음을 의미합니다.

## 테스트 케이스 실행

테스트 사례를 실행하려면 LoginServiceTest.java 클래스를 마우스 오른쪽 버튼으로 클릭하고 Run As > JUnit Test를 선택합니다.

콘솔에 다음 출력이 표시되어야 합니다.

```
. ____ _ __ _ _
 /\\ / ___'_ __ _ _(_)_ __ __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/ ___)| |_)| | | | | || (_| | ) ) ) )
  ' |____| .__|_| |_|_| |_\__, | / / / /
 =======|_|================|___/=/_/_/_/
 :: 스프링 부트 :: (v2.0.3.RELEASE)

2018-07-26 12:21:06.469 INFO 6484 --- [ main] c.e.j.t.s.LoginServiceTest : PID 6484로 PC-LAPTOP에서 LoginServiceTest 시작(C:\junit-tutorial에서 John Doe가 시작)
2018-07-26 12:21:06.470 INFO 6484 --- [ main] c.e.j.t.s.LoginServiceTest : 활성 프로필 세트 없음, 기본 프로필로 대체: 기본값
2018-07-26 12:21:06.526 정보 6484 --- [ main] s.c.a.AnnotationConfigApplicationContext: 새로 고침 org.springframework.context.annotation.AnnotationConfigApplicationContext@4a3a4df7: 시작 날짜 [Thu Jul 26 12:21:06 EDT 2018]; 컨텍스트 계층의 루트
2018-07-26 12:21:07.067 INFO 6484 --- [ main ] o.s.j.e.a.AnnotationMBeanExporter : 시작 시 JMX 노출을 위한 bean 등록
2018-07-26 12:21:07.068 INFO 6484 --- [ main] o.s.j.e.a.AnnotationMBeanExporter: 이름이 'dataSource'인 Bean이 JMX 노출에 대해 자동 감지되었습니다.
2018-07-26 12:21:07.069 INFO 6484 --- [ main ] o.s.j.e.a.AnnotationMBeanExporter : MBean 'dataSource' 위치: JMX 서버에 MBean으로 등록 [com.zaxxer.hikari:name=dataSource,type=HikariDataSource]
2018-07-26 12:21:07.076 정보 6484 --- [ main] o.s.b.a.h2.H2ConsoleAutoConfiguration : '/h2-console'에서 H2 콘솔을 사용할 수 있습니다. 'jdbc:h2:mem:testdb'에서 사용 가능한 데이터베이스
2018-07-26 12:21:07.094 정보 6484 --- [ 주] o.s.j.e.a.AnnotationMBeanExporter: MBean 'h2:name=MemoryManagerService' 위치: MBean으로 JMX 서버에 등록 [org.h2.mvstore.db.H2Database:name= 메모리매니저 서비스]
2018-07-26 12:21:07.095 INFO 6484 --- [ main ] o.s.j.e.a.AnnotationMBeanExporter : MBean 'h2:name=DatabaseStatusMBean' 위치: JMX 서버에 MBean으로 등록 [org.h2.engine.DatabaseStatusMBean]
2018-07-26 12:21:07.097 정보 6484 --- [ 주] o.s.j.e.a.AnnotationMBeanExporter: MBean 'h2:name=DeadlockDetector' 위치: JMX 서버에 MBean으로 등록 [org.h2.engine.DeadlockDetector]
2018-07-26 12:21:07.098 정보 6484 --- [ 주] o.s.j.e.a.AnnotationMBeanExporter: MBean 'h2:name=ThreadPool' 위치: MBean [org.h2.engine.ThreadPool]으로 JMX 서버에 등록
2018-07-26 12:21:07.102 정보 6484 --- [ main] o.s.j.e.a.AnnotationMBeanExporter: MBean 'h2:name=SessionTracker' 위치: JMX 서버에 MBean으로 등록 [org.h2.engine.SessionTracker]
2018-07-26 12:21:07.104 정보 6484 --- [ 주] o.s.j.e.a.AnnotationMBeanExporter: MBean 'h2:name=WebServer' 위치: JMX 서버에 MBean [org.h2.tools.Server]로 등록
2018-07-26 12:21:07.105 정보 6484 --- [ main] o.s.j.e.a.AnnotationMBeanExporter: MBean 'h2:name=ConnectionPool' 위치: MBean [org.h2.engine.ConnectionPool]으로 JMX 서버에 등록
2018-07-26 12:21:07.106 INFO 6484 --- [ main ] o.s.j.e.a.AnnotationMBeanExporter : MBean 'h2:name=StatementTracker' 위치: JMX 서버에 MBean으로 등록 [org.h2.engine.StatementTracker]
2018-07-26 12:21:07.107 정보 6484 --- [ 주] o.s.j.e.a.AnnotationMBeanExporter: MBean 'h2:name=SystemProperties' 위치: JMX 서버에 MBean [org.h2.engine.SystemProperties] 등록
2018-07-26 12:21:07.108 정보 6484 --- [ 주] o.s.j.e.a.AnnotationMBeanExporter: MBean 'h2:name=Versions' 위치: MBean [org.h2.engine.Versions]으로 JMX 서버에 등록
2018-07-26 12:21:07.109 정보 6484 --- [ 주] o.s.j.e.a.AnnotationMBeanExporter: MBean 'h2:name=ClusterSettings' 위치: JMX 서버에 MBean으로 등록 [org.h2.cluster.settings.ClusterSettings]
2018-07-26 12:21:07.110 INFO 6484 --- [ main] o.s.j.e.a.AnnotationMBeanExporter: MBean 'h2:name=ServerInfo' 위치: JMX 서버에 MBean [org.h2.engine.ServerInfo] 등록
2018-07-26 12:21:07.115 정보 6484 --- [주] o.s.b.w.embedded.tomcat.TomcatWebServer: 포트로 초기화된 Tomcat: 8080(http)
2018-07-26 12:21:07.118 INFO 6484 --- [main] o.apache.catalina.core.StandardService : 서비스 시작 [Tomcat]
2018-07-26 12:21:07.118 정보 6484 --- [ 주] org.apache.catalina.core.StandardEngine : 서블릿 엔진 시작: Apache Tomcat/8.5.27
2018-07-26 12:21:07.119 정보 6484 --- [ost-startStop-1] o.a.catalina.core.AprLifecycleListener : 프로덕션 환경에서 최적의 성능을 제공하는 APR 기반 Apache Tomcat Native 라이브러리가 Java에서 발견되지 않았습니다. 라이브러리.경로: [C:\Program Files\Java\jdk1.8.0_171\bin;C:\WINDOWS\Sun\Java\bin;C:\WINDOWS\system32;C:\WINDOWS;C:/Program Files/Java /jdk1.8.0_171/jre/bin/server;C:/프로그램 파일/Java/jdk1.8.0_171/jre/bin;C:/프로그램 파일/Java/jdk1.8.0_171/jre/lib/amd64;C: \ProgramData\Oracle\Java\javapath;C:\WINDOWS\system32;C:\WINDOWS;C:\WINDOWS\System32\Wbem;C:\WINDOWS\System32\WindowsPowerShell\v1.0\;C:\Program Files\ Git\cmd;C:\Program Files\nodejs\;C:\Program Files (x86)\Brackets\command;C:\Users\John Doe\AppData\Local\Microsoft\WindowsApps;;.]
2018-07-26 12:21:07.154 정보 6484 --- [ost-startStop-1] o.a.c.c.C.[Tomcat].[localhost].[/] : Spring 내장 WebApplicationContext 초기화
2018-07-26 12:21:07.154 정보 6484 --- [ost-startStop-1] o.s.web.context.ContextLoader : 루트 WebApplicationContext: 350ms 내에 초기화 완료
2018-07-26 12:21:07.295 정보 6484 --- [ost-startStop-1] o.s.b.w.servlet.ServletRegistrationBean: [/]에 매핑된 서블릿 디스패처Servlet
2018-07-26 12:21:07.296 정보 6484 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean: 매핑 필터: 'characterEncodingFilter' to: [/*]
2018-07-26 12:21:07.296 정보 6484 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean: 매핑 필터: 'hiddenHttpMethodFilter' to: [/*]
2018-07-26 12:21:07.296 정보 6484 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean: 매핑 필터: 'httpPutFormContentFilter' to: [/*]
2018-07-26 12:21:07.296 정보 6484 --- [ost-startStop-1] o.s.b.w.servlet.FilterRegistrationBean: 매핑 필터: 'requestContextFilter' to: [/*]
2018-07-26 12:21:07.363 정보 6484 --- [ main ] j.LocalContainerEntityManagerFactoryBean : 지속성 단위 'default'에 대한 JPA 컨테이너 EntityManagerFactory 빌드
2018-07-26 12:21:07.364 정보 6484 --- [ 주] o.hibernate.jpa.internal.util.LogHelper: HHH000204: PersistenceUnitInfo 처리 [
이름: 기본값
...]
2018-07-26 12:21:07.380 정보 6484 --- [주요] org.hibernate.Version: HHH000412: Hibernate Core {5.2.17.Final}
2018-07-26 12:21:07.381 정보 6484 --- [주요] org.hibernate.cfg.Environment: HHH000206: hibernate.properties를 찾을 수 없음
2018-07-26 12:21:07.381 INFO 6484 --- [main] org.hibernate.cfg.Environment: HHH000021: 바이트코드 공급자 이름: javassist
2018-07-26 12:21:07.402 정보 6484 --- [주요] o.hibernate.annotations.common.Version: HCANN000001: 최대 절전 모드 주석 {5.0.1.Final}
2018-07-26 12:21:07.445 정보 6484 --- [주요] org.hibernate.dialect.Dialect: HHH000400: 방언 사용: org.hibernate.dialect.H2Dialect
2018-07-26 12:21:07.502 정보 6484 --- [ main] o.h.e.j.e.i.LobCreatorBuilderImpl: HHH000424: 연결이 null이므로 컨텍스트 LOB 생성 비활성화
2018-07-26 12:21:07.504 정보 6484 --- [주] org.hibernate.type.BasicTypeRegistry: HHH000270: 유형 등록 [java.util.UUID]가 이전을 재정의함: org.hibernate.type.UUIDBinaryType@6e3c0c47
2018-07-26 12:21:07.620 INFO 6484 --- [ main ] o.s.j.e.a.AnnotationMBeanExporter : 시작 시 JMX 노출을 위한 bean 등록
2018-07-26 12:21:07.621 INFO 6484 --- [ main] o.s.j.e.a.AnnotationMBeanExporter: 이름이 'dataSource'인 Bean이 JMX 노출에 대해 자동 감지되었습니다.
2018-07-26 12:21:07.621 INFO 6484 --- [ main] o.s.j.e.a.AnnotationMBeanExporter: 이름이 'entityManagerFactory'인 Bean이 JMX 노출에 대해 자동 감지되었습니다.
2018-07-26 12:21:07.621 정보 6484 --- [ main ] o.s.j.e.a.An