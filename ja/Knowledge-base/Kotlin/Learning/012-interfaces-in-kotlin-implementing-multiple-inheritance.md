---
title: 012: Kotlin のインターフェイス: 多重継承の実装
description: 
published: true
date: 2023-01-31T05:42:56.965Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:42:53.575Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [012: Interfaces in Kotlin: Implementing Multiple Inheritance***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/012-interfaces-in-kotlin-implementing-multiple-inheritance)
{.links-list}



Kotlinは、JVM、Android、JavaScript、およびNativeを対象とした静的型プログラミング言語です。強力な機能を備えた実用的なオープンソース言語です。

Kotlinは既存のJavaコードと相互運用可能なため、開発者は簡単に起動できます。

この記事では、Kotlinのインターフェースとそれを使用して複数の継承を実装する方法について説明します。

## インターフェースとは？

インタフェースは、クラスが実行する必要があるアクションを指定する契約ですが、クラスの実行方法は指定しません。

インタフェースはKotlinの重要な機能であり、クラスが実装する必要がある動作を定義するために使用されます。

たとえば、車両を表すクラスがあるとします。このクラスは、車輪の数の属性と駆動機能を持つことができます。

```kotlin
interface Driveable {
    fun drive()
}

class Vehicle(val wheels: Int) : Driveable {
    override fun drive() {
        // drive the vehicle
    }
}
```

上記の例では、drive（）という単一の関数を持つDriveableというインターフェースを定義しました。次に、このインタフェースを実装する Vehicle というクラスを作成しました。

## インタフェースと継承

Kotlinのインターフェースは他のインターフェースから継承できます。これにより、複数のクラスで再利用できる複雑なインターフェイスを作成できます。

たとえば、道路上で運転できる車両用インターフェースと、水上で運転できる車両用インターフェースがあるとします。

```kotlin
interface Driveable {
    fun drive()
}

interface RoadVehicle: Driveable {
    fun driveOnRoad()
}

interface WaterVehicle: Driveable {
    fun driveOnWater()
}
```

上記の例では、drive（）という単一の関数を持つDriveableというインターフェースを定義しました。次に、Driveableから継承するRoadVehicleとWaterVehicleという2つのインターフェースを作成しました。

これで、これらのインタフェースをすべて実装するクラスを作成できます。

```kotlin
class AmphibiousVehicle(val wheels: Int) : RoadVehicle, WaterVehicle {
    override fun drive() {
        // drive the vehicle
    }

    override fun driveOnRoad() {
        // drive on the road
    }

    override fun driveOnWater() {
        // drive on the water
    }
}
```

上記の例では、RoadVehicle インターフェイスと WaterVehicle インターフェイスの両方を実装する AmphibiousVehicle というクラスを作成しました。

これにより、コードを複製せずにさまざまな状況で使用できるクラスを作成できます。

##結論

この記事では、Kotlinのインターフェースとそれを使用して複数の継承を実装する方法について説明しました。

インターフェイスは、複雑で再利用可能なコードを作成するために使用できる強力なツールです。

Kotlinを初めて使用する場合は、Kotlinに関するその他のドキュメントを確認して、この強力な言語の詳細を学ぶことをお勧めします。