---
title: Spring Boot 開発における Builder パターン
description: 
published: true
date: 2023-02-17T18:13:56.865Z
tags: 
editor: markdown
dateCreated: 2023-01-30T21:04:35.299Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [The Builder Pattern in Spring Boot Development***English** version of this document is available*](/en/Knowledge-base/Spring-Boot/the-builder-pattern-in-spring-boot-development)
{.links-list}


# Spring Boot開発のビルダーパターン

Spring Frameworkで作業するときは、複数のコンストラクタ引数を必要とする複雑なオブジェクトのインスタンスを作成する必要があることがよくあります。これにより、読みやすく保守が困難なコードが生成される可能性があります。ビルダー・パターンは、複雑なオブジェクトを徐々に構成するために使用できるビルダー・オブジェクトを作成することで、この問題を解決するために使用できるソフトウェア設計パターンです。

この記事では、Spring Boot開発でBuilderパターンをどのように使用するかを見てみましょう。また、このパターンを使用する際のいくつかの利点と欠点を見てみましょう。

## Builderパターンとは？

Builderパターンは、複数のコンストラクタ引数を必要とする複雑なオブジェクトを作成する方法を提供するソフトウェアデザインパターンです。オプションのパラメータが多いオブジェクトを作成する必要がある場合によく使用されます。

Builder パターンは、複数のコンストラクター引数を必要とする複雑なオブジェクトを作成する問題を解決するために使用される生成設計パターンです。ビルダーパターンは、オブジェクトの構成と表現を分離します。これにより、同じ構成プロセスで異なる表現を作成できます。

ビルダーパターンはファクトリパターンに似ていますが、いくつかの重要な違いがあります。ファクトリパターンはオブジェクトの作成に関連していますが、ビルダーパターンはオブジェクトの作成に関連しています。ファクトリパターンは、同じタイプのオブジェクトを作成する必要がある場合に使用されます。 Builder パターンは、異なるタイプのオブジェクトを作成する必要がある場合に使用されます。

Builder パターンには次の利点があります。

- オブジェクトの構成と表現を分離します。これにより、同じ構成プロセスで異なる表現を作成できます。
- 複雑なオブジェクトを段階的に作成できます。
- クライアントコードに影響を与えずに構成プロセスを変更できます。

Builder パターンには次の欠点があります。

- 多くの定型句コードにつながる可能性があります。
- ビルダーパターンを正しく使用しないと、結果コードを理解するのが難しい場合があります。

##ビルダーパターンはいつ使用されますか？

ビルダーパターンは、複数のコンストラクタ引数を必要とする複雑なオブジェクトを作成する必要がある場合に使用する必要があります。オプションのパラメータが多いオブジェクトを作成する必要がある場合によく使用されます。

## Spring BootでBuilderパターンを使用するには？

Spring Bootでは、Builderパターンを使用して、複数のコンストラクタ引数を必要とする複雑なオブジェクトを作成できます。 @ConfigurationProperties アノテーションは、プロパティを Builder オブジェクトにバインドするために使用できます。

以下は、Spring BootでBuilderパターンを使用する方法の例です。

```java
@ConfigurationProperties(prefix="acme")
public class AcmeProperties {

    private String name;

    private String email;

    private String phone;

    // Getters and setters

    public static class Builder {
        private String name;
        private String email;
        private String phone;

        public Builder withName(String name) {
            this.name = name;
            return this;
        }

        public Builder withEmail(String email) {
            this.email = email;
            return this;
        }

        public Builder withPhone(String phone) {
            this.phone = phone;
            return this;
        }

        public AcmeProperties build() {
            return new AcmeProperties(this);
        }
    }

    private AcmeProperties(Builder builder) {
        this.name = builder.name;
        this.email = builder.email;
        this.phone = builder.phone;
    }

    // Getters and setters

}
```

@ConfigurationProperties アノテーションは、プロパティを Builder オブジェクトにバインドするために使用されます。 withName()、withEmail() および withPhone() メソッドは、名前、電子メール、および電話プロパティの値を設定するために使用されます。 build() メソッドは、AcmeProperties クラスのインスタンスを作成するために使用されます。

AcmeProperties クラスの使用方法の例を次に示します。

```java
@Autowired
private AcmeProperties acmeProperties;

@Test
public void test() {
    AcmeProperties.Builder builder = new AcmeProperties.Builder();
    builder.withName("John Smith")
           .withEmail("john.smith@example.com")
           .withPhone("555-555-1212");
    AcmeProperties acmeProperties = builder.build();
    assertThat(acmeProperties.getName()).isEqualTo("John Smith");
    assertThat(acmeProperties.getEmail()).isEqualTo("john.smith@example.com");
    assertThat(acmeProperties.getPhone()).isEqualTo("555-555-1212");
}
```

上記の例では、AcmeProperties クラスを使用して AcmeProperties クラスのインスタンスを作成します。 withName()、withEmail() および withPhone() メソッドは、名前、電子メール、および電話プロパティの値を設定するために使用されます。 build() メソッドは、AcmeProperties クラスのインスタンスを作成するために使用されます。

Builder パターンを使用して、複数のコンストラクター引数を必要とする複雑なオブジェクトを作成できます。 @ConfigurationProperties アノテーションは、プロパティを Builder オブジェクトにバインドするために使用できます。 withName()、withEmail() および withPhone() メソッドは、名前、電子メール、および電話プロパティの値を設定するために使用されます。 build() メソッドは、AcmeProperties クラスのインスタンスを作成するために使用されます。