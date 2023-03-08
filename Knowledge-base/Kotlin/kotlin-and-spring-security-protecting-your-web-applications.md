---
title: Kotlin 및 Spring Security: 웹 애플리케이션 보호
description: 
published: true
date: 2023-01-31T12:44:09.813Z
tags: 
editor: markdown
dateCreated: 2023-01-31T12:44:08.213Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Kotlin and Spring Security: Protecting Your Web Applications***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-spring-security-protecting-your-web-applications)
{.links-list}



# Kotlin과 Spring Security: 웹 애플리케이션 보호

웹 개발을 위해 점점 더 많은 개발자가 Kotlin으로 전환하고 있습니다. Kotlin은 Java Virtual Machine에서 실행되는 간결하고 안전하며 상호 운용이 가능하고 도구 친화적인 언어입니다.

Spring Security는 강력하고 사용자 정의가 가능한 인증 및 액세스 제어 프레임워크입니다. 이는 Spring 기반 애플리케이션 보안을 위한 사실상의 표준입니다.

이 기사에서는 Kotlin 및 Spring Security를 사용하여 웹 애플리케이션을 보호하는 방법을 살펴봅니다. Spring Security를 구성하고 Kotlin 코드를 작성하여 인증, 권한 부여 및 비밀번호 암호화와 같은 일반적인 보안 기능을 구현하는 방법을 살펴보겠습니다.

## 스프링 보안 설정

 Spring Security는 Java 또는 Kotlin 코드를 사용하여 구성할 수 있습니다. 이 섹션에서는 Kotlin을 사용하여 Spring Security를 구성하는 방법을 살펴보겠습니다.

### 스프링 보안 종속성 추가

프로젝트에 Spring Security를 추가하려면 `build.gradle.kts` 파일에 다음 종속 항목을 추가하세요.

```kotlin
implementation("org.springframework.boot:spring-boot-starter-security")
implementation("org.springframework.security.oauth.boot:spring-security-oauth2-autoconfigure")
```

### SecurityConfig 클래스 만들기

다음으로 Spring Security를 구성하기 위해 `SecurityConfig` 클래스를 생성합니다. 이 클래스는 `WebSecurityConfigurerAdapter`를 확장하고 `configure` 메서드를 재정의합니다.

```kotlin
@Configuration
@EnableWebSecurity
class SecurityConfig : WebSecurityConfigurerAdapter() {

    override fun configure(http: HttpSecurity) {
        // ...
    }
}
```

`configure` 메소드에서는 인증, 권한 부여 및 세션 관리와 같은 Spring Security의 다양한 측면을 구성할 수 있습니다.

### 인증 구성

Spring Security는 간단한 사용자 이름/암호 인증에서 OAuth2 및 LDAP와 같은 보다 정교한 메커니즘에 이르기까지 광범위한 인증 메커니즘을 지원합니다.

이 예제에서는 사용자 이름/암호 인증을 사용하도록 Spring Security를 구성합니다. `UserDetailsService` 인터페이스를 사용하여 데이터베이스에 사용자 이름과 암호를 저장합니다.

```kotlin
@Configuration
@EnableWebSecurity
class SecurityConfig : WebSecurityConfigurerAdapter() {

    override fun configure(http: HttpSecurity) {
        http.authorizeRequests()
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .and()
            .httpBasic()
                .and()
            .logout()
    }

    @Autowired
    fun configureGlobal(auth: AuthenticationManagerBuilder) {
        auth.inMemoryAuthentication()
                .withUser("user").password("{noop}password").roles("USER")
    }
}
```

위의 코드에서 사용자 이름/비밀번호 인증을 사용하도록 Spring Security를 구성했습니다. 또한 사용자 이름과 비밀번호를 메모리에 저장하도록 `UserDetailsService`를 구성했습니다.

### 인증 구성

사용자가 인증되면 애플리케이션 내에서 수행할 수 있는 작업을 제어하도록 인증을 구성해야 합니다.

Spring Security는 두 가지 유형의 인증을 지원합니다.

* 역할 기반 인증: 사용자의 역할은 애플리케이션 내에서 수행할 수 있는 작업을 결정합니다.
* 리소스 기반 인증: 사용자의 권한은 애플리케이션 내에서 수행할 수 있는 작업을 결정합니다.

이 예에서는 역할 기반 인증을 구성합니다. `USER` 및 `ADMIN`의 두 가지 역할을 구성합니다. `USER` 역할을 가진 사용자는 `/user` 엔드포인트에 액세스할 수 있고 `ADMIN` 역할을 가진 사용자는 `/admin` 엔드포인트에 액세스할 수 있습니다.

```kotlin
@Configuration
@EnableWebSecurity
class SecurityConfig : WebSecurityConfigurerAdapter() {

    override fun configure(http: HttpSecurity) {
        http.authorizeRequests()
                .antMatchers("/user").hasRole("USER")
                .antMatchers("/admin").hasRole("ADMIN")
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .and()
            .httpBasic()
                .and()
            .logout()
    }

    @Autowired
    fun configureGlobal(auth: AuthenticationManagerBuilder) {
        auth.inMemoryAuthentication()
                .withUser("user").password("{noop}password").roles("USER")
                .and()
                .withUser("admin").password("{noop}password").roles("ADMIN")
    }
}
```

위의 코드에서 `hasRole` 메서드를 사용하여 역할 기반 인증을 구성했습니다. 또한 사용자 이름과 비밀번호를 메모리에 저장하도록 `UserDetailsService`를 구성했습니다.

### 암호 암호화 구성

Spring Security는 광범위한 암호 암호화 알고리즘을 지원합니다. 이 예제에서는 `bcrypt` 알고리즘을 사용하도록 Spring Security를 구성합니다.

```kotlin
@Configuration
@EnableWebSecurity
class SecurityConfig : WebSecurityConfigurerAdapter() {

    override fun configure(http: HttpSecurity) {
        http.authorizeRequests()
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .and()
            .httpBasic()
                .and()
            .logout()
                .and()
            .apply {
                passwordEncoder(BCryptPasswordEncoder())
            }
    }

    @Autowired
    fun configureGlobal(auth: AuthenticationManagerBuilder) {
        auth.inMemoryAuthentication()
                .withUser("user").password("{noop}password").roles("USER")
                .and()
                .withUser("admin").password("{noop}password").roles("ADMIN")
    }
}
```

위의 코드에서 'BCryptPasswordEncoder'를 사용하여 비밀번호를 암호화하도록 Spring Security를 구성했습니다. 또한 사용자 이름과 비밀번호를 메모리에 저장하도록 `UserDetailsService`를 구성했습니다.

## Kotlin 코드 작성

이 섹션에서는 인증, 권한 부여 및 비밀번호 암호화와 같은 일반적인 보안 기능을 구현하기 위해 Kotlin 코드를 작성하는 방법을 살펴보겠습니다.

### 사용자 인증

사용자를 인증하기 위해 `authenticationManager.authenticate` 메서드를 사용합니다.

```kotlin
@Configuration
@EnableWebSecurity
class SecurityConfig : WebSecurityConfigurerAdapter() {

    override fun configure(http: HttpSecurity) {
        http.authorizeRequests()
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .and()
            .httpBasic()
                .and()
            .logout()
    }

    @Autowired
    fun configureGlobal(auth: AuthenticationManagerBuilder) {
        auth.inMemoryAuthentication()
                .withUser("user").password("{noop}password").roles("USER")
                .and()
                .withUser("admin").password("{noop}password").roles("ADMIN")
    }

    @Autowired
    fun authenticationManager(): AuthenticationManager {
        return authenticationManager()
    }
}
```

위의 코드에서 `AuthenticationManager`를 `SecurityConfig` 클래스에 삽입했습니다. 그런 다음 `authenticationManager.authenticate` 메서드를 사용하여 사용자를 인증할 수 있습니다.

### 사용자 인증

사용자에게 권한을 부여하려면 `hasRole` 메소드를 사용합니다.

```kotlin
@Configuration
@EnableWebSecurity
class SecurityConfig : WebSecurityConfigurerAdapter() {

    override fun configure(http: HttpSecurity) {
        http.authorizeRequests()
                .antMatchers("/user").hasRole("USER")
                .antMatchers("/admin").hasRole("ADMIN")
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .and()
            .httpBasic()
                .and()
            .logout()
    }

    @Autowired
    fun configureGlobal(auth: AuthenticationManagerBuilder) {
        auth.inMemoryAuthentication()
                .withUser("user").password("{noop}password").roles("USER")
                .and()
                .withUser("admin").password("{noop}password").roles("ADMIN")
    }
}
```

위의 코드에서 `hasRole` 메서드를 사용하여 사용자를 인증했습니다. 또한 사용자 이름과 비밀번호를 메모리에 저장하도록 `UserDetailsService`를 구성했습니다.

### 암호 암호화

암호를 암호화하기 위해 `passwordEncoder` 메서드를 사용합니다.

```kotlin
@Configuration
@EnableWebSecurity
class SecurityConfig : WebSecurityConfigurerAdapter() {

    override fun configure(http: HttpSecurity) {
        http.authorizeRequests()
                .anyRequest().authenticated()
                .and()
            .formLogin()
                .and()
            .httpBasic()
                .and()
            .logout()
                .and()
            .apply {
                passwordEncoder(BCryptPasswordEncoder())
            }
    }

    @Autowired
    fun configureGlobal(auth: AuthenticationManagerBuilder) {
        auth.inMemoryAuthentication()
                .withUser("user").password("{noop}password").roles("USER")
                .and()
                .withUser("admin").password("{noop}password").roles("ADMIN")
    }
}
```

위의 코드에서 비밀번호를 암호화하기 위해 `passwordEncoder` 메서드를 사용했습니다. 또한 사용자 이름과 비밀번호를 메모리에 저장하도록 `UserDetailsService`를 구성했습니다.

## 결론

이 기사에서는 Kotlin과 Spring Security를 사용하여 웹 애플리케이션을 보호하는 방법을 살펴보았습니다. Spring Security를 구성하고 Kotlin 코드를 작성하여 인증, 권한 부여 및 비밀번호 암호화와 같은 일반적인 보안 기능을 구현하는 방법을 살펴보았습니다.