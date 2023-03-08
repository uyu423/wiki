---
title: 030: Kotlin の文字列テンプレート: 式による文字列の補間
description: 
published: true
date: 2023-02-01T05:04:48.192Z
tags: 
editor: markdown
dateCreated: 2023-02-01T05:04:46.509Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [030: String Templates in Kotlin: Interpolating Strings with Expressions***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/030-string-templates-in-kotlin-interpolating-strings-with-expressions)
{.links-list}




# Kotlinの文字列テンプレート：式で文字列補間

Kotlinの文字列テンプレートは、文字列内で式を補間する簡単で便利な方法を提供します。これは、ユーザー名や現在の日付などの文字列に動的コンテンツを挿入する必要がある場合に便利です。

文字列テンプレートは、ドル記号 `$`で始まり、その後に中括弧 `{}`で囲まれた式が続きます。式は有効なKotlinコードにすることができ、評価され、結果が文字列に挿入されます。

たとえば、次の文字列テンプレートは次のようになります。

```kotlin
val name="John"
println("Hello, $name!")
```

「Hello, John!」を出力します。

文字列テンプレートを使用して関数呼び出しの結果を挿入することもできます。

```kotlin
fun getCurrentDate(): String {
    // ...
}

println("Today is $getCurrentDate().")
```

式が複雑な式の場合は、 `$`文字を使用してメンバーにアクセスできます。

```kotlin
data class User(val name: String, val age: Int)

val user = User("John", 30)
println("User $user.name is $user.age years old.")
```

その後、「ユーザージョンは30歳です」と印刷されます。

文字列テンプレートを使用して関数呼び出しの結果を挿入することもできます。

```kotlin
fun getCurrentDate(): String {
    // ...
}

println("Today is $getCurrentDate().")
```

式が複雑な式の場合は、 `$`文字を使用してメンバーにアクセスできます。

```kotlin
data class User(val name: String, val age: Int)

val user = User("John", 30)
println("User $user.name is $user.age years old.")
```

その後、「ユーザージョンは30歳です」と印刷されます。

`${}`構文を使用して複雑な式を補間することもできます。

```kotlin
data class User(val name: String, val age: Int)

val user = User("John", 30)
println("User ${user.name} is ${user.age} years old.")
```

これは前の例と同じです。

## 中かっこエスケープ

文字列テンプレートにリテラル `$` または `{` 文字を挿入する必要がある場合は、バックスラッシュ `\` でエスケープできます。

```kotlin
println("\${5 + 5}") // prints ${5 + 5}
println("\$5 + 5") // prints $5 + 5
```

バックスラッシュ文字を挿入する必要がある場合は、別のバックスラッシュにエスケープできます。

```kotlin
println("\\") // prints \
```

## 空白の切り抜き

デフォルトでは、文字列テンプレートは補間された式で先行または末尾のスペースを保持します。この空白を削除するには、 `trimIndent()` または `trimMargin()` メソッドを使うことができます。

```kotlin
val text = """
    |Lorem ipsum dolor sit amet,
    |consectetur adipiscing elit。
    |""".trimMargin()

println(text) // prints Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

`trimIndent()` メソッドはすべての先行スペースを削除しますが、 `trimMargin()` メソッドは各行の最初の非スペース文字まですべての先行スペースを削除します。上記の例では、この文字は `|`です。

## 安全な通貨

文字列テンプレートでnullable式を補間すると、Kotlinは自動的に安全な呼び出し `?.`を挿入してNullPointerExceptionを防ぎます。

```kotlin
fun getUserName(): String? {
    // ...
}

println("User name is ${getUserName()}.")
```

`getUserName()` 関数が `null` を返すと、 `User name is null.` が出力されます。

## Null以外のアサーション

式が `null` ではないと確信している場合は、null 以外のアサーション演算子 `!!` を使用して安全な呼び出しを無効にできます。

```kotlin
fun getUserName(): String? {
    // ...
}

println("User name is ${getUserName()!!}.")
```

`getUserName()` 関数が `null` を返すと、 `User name is null.` が出力されます。

##結論

Kotlinの文字列テンプレートは、文字列内で式を補間する簡単で便利な方法を提供します。これは、ユーザー名や現在の日付などの文字列に動的コンテンツを挿入する必要がある場合に便利です。