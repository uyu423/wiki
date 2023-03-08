---
title: 011: Kotlin のプロパティとフィールド: ゲッターとセッターを理解する
description: 
published: true
date: 2023-01-31T05:36:58.404Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:36:54.270Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [011: Properties and Fields in Kotlin: Understanding Getters and Setters***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/011-properties-and-fields-in-kotlin-understanding-getters-and-setters)
{.links-list}


#Kotlinのプロパティとフィールド：GetterとSetterについて

Kotlinでは、プロパティとフィールドはカスタムゲッターとセッターを持つことができます。デフォルトでは、プロパティとフィールドはパブリックの可視性を持ち、これはクラスの外部からアクセスできることを意味します。

## 属性

属性は `val` キーワードを使用して宣言されます。変更できません。つまり、一度だけ割り当てることができます。

```kotlin
val name="John"
```

上記の例では、「name」属性は値「John」に初期化されています。上書きできません。

##フィールド

フィールドは `var` キーワードを使って宣言されます。変更可能なので再割り当てできます。

```kotlin
var name="John"
name="Jane"
```

上記の例では、`name`フィールドは値「John」に初期化されています。 「ジェーン」に再割り当てできます。

## ゲッターとセッター

デフォルトでは、プロパティとフィールドはパブリックの可視性を持ち、これはクラスの外部からアクセスできることを意味します。ただし、カスタムゲッターとセッターを作成してアクセス方法を制御できます。

Getter は、属性またはフィールドの値を取得するために使用されます。コードで属性またはフィールドを使用すると呼び出されます。

Setter は、属性またはフィールドの値を再割り当てするために使用されます。コード内で属性またはフィールドを再割り当てすると呼び出されます。

次の属性を考慮してください。

```kotlin
var name: String = "John"
```

次のように、このプロパティのカスタムゲッターとセッターを作成できます。

```kotlin
var name: String = "John"
    get() {
        return field
    }
    set(value) {
        field = value
    }
```

上記の例では、 `get()` 関数は getter で、 `set(value)` 関数は setter です。 `get()` 関数は `name` フィールドの値を返し、 `set(value)` 関数は `name` フィールドの値を設定します。

`val`キーワードで宣言された属性とフィールドのカスタムゲッターとセッターを作成することもできます。この場合、カスタムゲッターのみを作成できます。プロパティが変更できないため、カスタムセッターを作成できません。

次の属性を考慮してください。

```kotlin
val name: String = "John"
```

次のように、このプロパティ用のカスタムゲッターを作成できます。

```kotlin
val name: String = "John"
    get() {
        return field
    }
```

上記の例では、関数 `get()` は getter です。 `get()` 関数は `name` フィールドの値を返します。

##結論

Kotlinでは、プロパティとフィールドはカスタムゲッターとセッターを持つことができます。 Getterは属性またはフィールドの値を取得するために使用され、setterは属性またはフィールドの値を再割り当てするために使用されます。