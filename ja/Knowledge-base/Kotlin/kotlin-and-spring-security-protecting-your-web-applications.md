---
title: Kotlin と Spring のセキュリティ: Web アプリケーションの保護
description: 
published: true
date: 2023-01-31T12:44:09.947Z
tags: 
editor: markdown
dateCreated: 2023-01-31T12:44:08.234Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [Kotlin and Spring Security: Protecting Your Web Applications***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-spring-security-protecting-your-web-applications)
{.links-list}



# KotlinとSpring Security：Webアプリケーションの保護

Web開発のために、ますます多くの開発者がKotlinに移行しています。 Kotlinは、Java Virtual Machine上で動作する簡潔で安全で相互運用可能でツールに優しい言語です。

Spring Securityは、強力でカスタマイズ可能な認証およびアクセス制御フレームワークです。これはSpringベースのアプリケーションセキュリティのための事実上の標準です。

この記事では、KotlinとSpring Securityを使用してWebアプリケーションを保護する方法について説明します。 Spring Securityを設定し、Kotlinコードを書いて、認証、許可、パスワード暗号化などの一般的なセキュリティ機能を実装する方法を見てみましょう。

## Spring Securityの設定

 Spring Securityは、JavaコードまたはKotlinコードを使用して設定できます。このセクションでは、Kotlinを使用してSpring Securityを設定する方法について説明します。

### Springセキュリティ依存関係の追加

プロジェクトにSpring Securityを追加するには、 `build.gradle.kts`ファイルに次の依存関係を追加します。

```kotlin
implementation("org.springframework.boot:spring-boot-starter-security")
implementation("org.springframework.security.oauth.boot:spring-security-oauth2-autoconfigure")
```

### SecurityConfigクラスの作成

次に、Spring Securityを設定するために `SecurityConfig`クラスを作成します。このクラスは `WebSecurityConfigurerAdapter` を拡張し、 `configure` メソッドをオーバーライドします。

```kotlin
@Configuration
@EnableWebSecurity
class SecurityConfig : WebSecurityConfigurerAdapter() {

    override fun configure(http: HttpSecurity) {
        // ...
    }
}
```

`configure`メソッドでは、認証、承認、セッション管理など、Spring Securityのさまざまな側面を設定できます。

### 認証の設定

Spring Securityは、単純なユーザー名/パスワード認証からOAuth2やLDAPなどのより洗練されたメカニズムまで、幅広い認証メカニズムをサポートしています。

この例では、ユーザー名/パスワード認証を使用するようにSpring Securityを構成します。 `UserDetailsService`インタフェースを使用してデータベースにユーザー名とパスワードを保存します。

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

上記のコードでユーザー名/パスワード認証を使用するようにSpring Securityを設定しました。また、ユーザー名とパスワードをメモリに保存するように `UserDetailsService`を設定しました。

### 認証の設定

ユーザーが認証されると、アプリケーション内で実行できる操作を制御するように認証を構成する必要があります。

Spring Securityは2種類の認証をサポートしています。

*役割ベースの認証：ユーザーの役割は、アプリケーション内で実行できる操作を決定します。
*リソースベースの認証：ユーザーの権限は、アプリケーション内で実行できる操作を決定します。

この例では、役割ベースの認証を構成します。 「USER」と「ADMIN」の2つの役割を構成します。 `USER`ロールを持つユーザーは`/user`エンドポイントにアクセスでき、`ADMIN`ロールを持つユーザーは `/admin`エンドポイントにアクセスできます。

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

上記のコードでは、 `hasRole`メソッドを使用して役割ベースの認証を設定しました。また、ユーザー名とパスワードをメモリに保存するように `UserDetailsService`を設定しました。

### パスワード暗号化の設定

Spring Securityは幅広い暗号暗号化アルゴリズムをサポートしています。この例では、 `bcrypt`アルゴリズムを使用するようにSpring Securityを設定します。

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

上記のコードでは、「BCryptPasswordEncoder」を使用してパスワードを暗号化するようにSpring Securityを設定しました。また、ユーザー名とパスワードをメモリに保存するように `UserDetailsService`を設定しました。

## Kotlinコードを書く

このセクションでは、認証、許可、パスワード暗号化などの一般的なセキュリティ機能を実装するためにKotlinコードを書く方法について説明します。

### ユーザー認証

ユーザーを認証するには `authenticationManager.authenticate` メソッドを使用します。

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

上記のコードでは、 `AuthenticationManager`を `SecurityConfig`クラスに挿入しました。その後、 `authenticationManager.authenticate`メソッドを使用してユーザーを認証できます。

### ユーザー認証

ユーザーに権限を付与するには、`hasRole`メソッドを使用してください。

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

上記のコードでは、 `hasRole`メソッドを使用してユーザーを認証しました。また、ユーザー名とパスワードをメモリに保存するように `UserDetailsService`を設定しました。

###パスワード暗号化

パスワードを暗号化するために `passwordEncoder`メソッドを使用してください。

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

上記のコードでパスワードを暗号化するために `passwordEncoder`メソッドを使用しました。また、ユーザー名とパスワードをメモリに保存するように `UserDetailsService`を設定しました。

##結論

この記事では、KotlinとSpring Securityを使用してWebアプリケーションを保護する方法について説明しました。 Spring Securityを設定し、Kotlinコードを書いて、認証、許可、パスワード暗号化などの一般的なセキュリティ機能を実装する方法を見てきました。