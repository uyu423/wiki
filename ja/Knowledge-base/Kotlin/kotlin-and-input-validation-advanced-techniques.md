---
title: Kotlin と入力検証: 高度なテクニック
description: 
published: true
date: 2023-02-17T18:03:05.556Z
tags: 
editor: markdown
dateCreated: 2023-01-30T10:29:33.406Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Kotlin and Input Validation: Advanced Techniques***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-input-validation-advanced-techniques)
{.links-list}
 

# Kotlinと入力検証：高度な技術

ユーザー入力の検証は、デスクトップアプリ、Webアプリ、モバイルアプリなど、あらゆるアプリケーションにとって重要な部分です。この記事では、Kotlinで入力を検証するいくつかの高度な技術を見ていきます。

入力検証の基本を確認することから始めましょう。次に、正規表現やカスタムバリデータの使用など、いくつかの高度な技術を見てみましょう。最後に、よりメンテナンスと再利用可能なコードを書くためのいくつかのヒントで終わります。

##レビュー：入力検証の基本

入力検証は、ユーザーが提供したデータがアプリケーションの要件を満たしていることを確認するプロセスです。これらの要件は、データ型（整数のみ）から形式（電子メールアドレスには「@」記号を含める必要があります）、長さ（パスワードは8文字以上でなければなりません）まで、何でもかまいません。

入力検証は、次の2つの主な理由で重要です。

- **セキュリティ：**誤ったデータは、アプリケーションの脆弱性を悪用するために使用される可能性があります。たとえば、メールアドレスを確認しないと、悪意のあるユーザーが ``>>example.com<script>alert('xss')</script>'' などのメールアドレスを入力する可能性があります。これでXSSが生成されます。攻撃。

- **データ品質：**誤ったデータが原因でアプリケーションが誤動作する可能性があります。たとえば、フィールドが整数であることを確認しないと、データに対して数学演算を実行しようとすると予期しない結果が発生する可能性があります。

Kotlinには入力を検証するさまざまな方法があります。最も基本的な方法は、`is`演算子を使用して変数のデータ型を確認することです。

```kotlin
fun validateInput(input: Any) {
    if(input is String) {
        // The input is a string, so we can validate its length, format, etc.
    } else if(input is Int) {
        // The input is an integer, so we can validate that it's in the correct range, etc.
    }else{
        // The input is not a string or an integer, so we can't validate it.
    }
}
```

`is`演算子は、カスタムデータ型を含むすべてのデータ型と一緒に使用できます。たとえば、`User`データクラスがある場合は、`is`演算子を使用して入力が`User`であることを確認できます。

```kotlin
fun validateInput(input: Any) {
    if(input is User) {
        // The input is a User, so we can validate its properties, etc.
    }else{
        // The input is not a User, so we can't validate it.
    }
}
```

「is」演算子に加えて、Kotlinは入力を検証するために使用できる「when」式も提供します。 `when`式は他の言語の `switch`ステートメントに似ていますが、すべてのデータ型と一致させることができるので、より強力です。

```kotlin
fun validateInput(input: Any) {
    when(input){
        is String -> {
            // The input is a string, so we can validate its length, format, etc.
        }
        is Int -> {
            // The input is an integer, so we can validate that it's in the correct range, etc.
        }
        else -> {
            // The input is not a string or an integer, so we can't validate it.
        }
    }
}
```

`is`演算子と同様に、`when`式もカスタムデータ型で使用できます。たとえば、`User`データクラスがある場合は、`when`式を使用して入力が`User`であることを確認できます。

```kotlin
fun validateInput(input: Any) {
    when(input){
        is User -> {
            // The input is a User, so we can validate its properties, etc.
        }
        else -> {
            // The input is not a User, so we can't validate it.
        }
    }
}
```

##高度な技術

###正規表現の使用

正規表現（regex）は入力を検証する強力なツールです。 Regexは、データ型（整数のみ）、形式（電子メールアドレスには「@」記号を含める必要があります）、長さ（パスワードは8文字以上でなければなりません）を検証するために使用できます。

Kotlinでは、 `Regex`クラスを使用して正規表現パターンを作成できます。

```kotlin
val regexPattern = Regex("^\\d+$") // This regex pattern matches integers only.
```

正規表現パターンがある場合は、 `matches`関数を使用して文字列がパターンと一致することを確認できます。

```kotlin
fun validateInput(input: String) {
    if(regexPattern.matches(input)) {
        // The input matches the regex pattern, so it's valid.
    }else{
        // The input doesn't match the regex pattern, so it's invalid.
    }
}
```

### カスタムバリデータの使用

`is`演算子と`when`式に加えて、Kotlinは入力を検証するために使用できる `validate`関数も提供します。 'validate' 関数は 'Validator<T>' を引数として使用します。ここで、 'T' は入力のデータ型です。

「Validator<T>」は、「入力：T」を引数として使用し、「ValidationResult」を返す「validate」関数を含むクラスです。 「ValidationResult」は、「Valid」と「Invalid」の2つの値を含む列挙型です。

以下は、整数が1から10の範囲にあることを確認する `Validator<Int>`の例です。

```kotlin
class IntRangeValidator(val min: Int, val max: Int) : Validator<Int> {
    override fun validate(input: Int): ValidationResult {
        return if(input in min..max) {
            ValidationResult.Valid
        }else{
            ValidationResult.Invalid
        }
    }
}
```

バリデータを使用するには、バリデータと入力とともに `validate` 関数を呼び出します。

```kotlin
fun validateInput(input: Int) {
    val validationResult = validate(IntRangeValidator(1, 10), input)
    if(validationResult == ValidationResult.Valid) {
        // The input is valid.
    }else{
        // The input is invalid.
    }
}
```

##メンテナンスと再利用可能なコードを書くためのヒント

入力検証は時間がかかり、エラーが発生しやすいプロセスになる可能性があります。幸いなことに、人生をより簡単にするためにできることがいくつかあります。

### 既存ライブラリの使用

入力検証を処理できる多くのライブラリがあります。可能であれば、独自のコードを記述する代わりに、これらのライブラリのいずれかを使用してください。

たとえば、Kotlin標準ライブラリには、データ型、型、および長さを検証するための一連の関数が含まれています。

```kotlin
fun validateString(input: String) {
    // Validates that the input is a string.
}

fun validateEmail(input: String) {
    // Validates that the input is a valid email address.
}

fun validatePassword(input: String) {
    // Validates that the input is a valid password.
}
```

### 保持可能なコードの記述

入力検証コードを書くときは、メンテナンス可能なコードを書くことが重要です。これは、読みやすく、理解しやすく、変更しやすいコードを意味します。

コードをより保守しやすくする1つの方法は、説明を含む変数名を使用することです。たとえば、 `input`を使用するのではなく、 `emailAddress`などのより説明的な名前を使用してください。

```kotlin
fun validateEmail(emailAddress: String) {
    // Validates that the email address is valid.
}
```

コードを維持しやすくする別の方法は、コメントを使用することです。コメントは、コードが何をしているのか、その理由を説明するために使用できます。たとえば、

```kotlin
// This regex pattern matches email addresses that contain a '@' symbol.
val regexPattern = Regex("^[^@]+@[^@]+$")

fun validateEmail(input: String) {
    if(regexPattern.matches(input)) {
        // The input is a valid email address.
    }else{
        // The input is not a valid email address.
    }
}
```

### 再利用可能なコードの記述

再利用可能なコードを書くことも重要です。これは、変更せずにさまざまな場所で使用できるコードを意味します。

コードをより再利用可能にする1つの方法は、さまざまな場所で使用できる関数とクラスを作成することです。たとえば、データ型、型、長さを検証する関数を含む `ValidationUtils` クラスを作成できます。

```kotlin
class ValidationUtils {
    fun validateString(input: String) {
        // Validates that the input is a string.
    }

    fun validateEmail(input: String) {
        // Validates that the input is a valid email address.
    }

    fun validatePassword(input: String) {
        // Validates that the input is a valid password.
    }
}
```

コードをより再利用可能にする別の方法は、拡張機能を作成することです。拡張関数は、既存のデータ型に追加できる関数です。たとえば、文字列が有効な電子メールアドレスであることを確認する `String` データ型の拡張機能を作成できます。

```kotlin
fun String.isValidEmail(): Boolean {
    // Validates that the input is a valid email address.
    return this.contains("@")
}
```

##結論

この記事では、Kotlinで入力を検証するいくつかの高度な技術について説明しました。入力検証の基礎を確認し、正規表現とカスタムバリデータの使用を含むいくつかの高度な技術を検討しました。最後に、よりメンテナンスと再利用可能なコードを書くためのいくつかのヒントで仕上げました。