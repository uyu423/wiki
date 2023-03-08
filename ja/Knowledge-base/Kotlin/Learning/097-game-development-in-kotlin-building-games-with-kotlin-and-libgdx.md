---
title: 097: Kotlin でのゲーム開発: Kotlin と LibGDX を使用したゲームのビルド
description: 
published: true
date: 2023-01-31T20:38:18.624Z
tags: 
editor: markdown
dateCreated: 2023-01-31T20:38:16.829Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}

- [097: Game Development in Kotlin: Building Games with Kotlin and LibGDX***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/097-game-development-in-kotlin-building-games-with-kotlin-and-libgdx)
{.links-list}


#097：Kotlinでゲームを開発する：KotlinとLibGDXでゲームを作る

Kotlinは、簡潔な構文とJavaとの相互運用性で人気を集めているJVM言語です。この記事では、LibGDXライブラリでゲーム開発にKotlinを使用する方法について説明します。

LibGDXは、複数のプラットフォームで統合APIを提供するクロスプラットフォームのゲーム開発ライブラリです。 Android、iOS、デスクトップ、HTML5をサポートします。 LibGDXアプリケーションはJavaで書かれていますが、GDX-Kotlinラッパーライブラリの代わりにKotlinを使用できます。

GDX-KotlinはLibGDX用のKotlinラッパーです。 LibGDX用のKotlin拡張とユーティリティを提供します。 GDX-Kotlinを使用すると、LibGDXでKotlinを簡単に使用できます。

LibGDXでKotlinを使用するには、プロジェクトにGDX-Kotlinライブラリを追加する必要があります。 build.gradle ファイルに以下を追加することで、Gradle でこれを行うことができます。

「groovy
repositories {
    mavenCentral()
}

dependencies {
    implementation "org.jetbrains.kotlin:kotlin-stdlib:$kotlin_version"
    implementation "org.jetbrains.kotlin:kotlin-reflect:$kotlin_version"
    implementation "com.badlogicgames.gdx:gdx-kotlin:$gdx_version"
}
```

また、プロジェクトにKotlinプラグインを追加する必要があります。 build.gradle ファイルに以下を追加するだけです。

「groovy
buildscript {
    ext.kotlin_version = '1.3.50'
    repositories {
        mavenCentral()
    }
    dependencies {
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:$kotlin_version"
    }
}
```

これでプロジェクトが設定されたので、LibGDXを使ってKotlinで簡単なゲームを書いてみましょう。

##シンプルなゲーム

LibGDXを使ってKotlinで簡単なゲームを書くことから始めましょう。私たちのゲームは2Dフラットフォーマーになります。プレイヤーは左右に移動し、ジャンプし、発射体を撃つことができます。

ゲームのクラスを定義することから始めましょう。クラスを `Game`と呼びます。

```kotlin
class Game : ApplicationAdapter() {
}
```

私たちの `Game` クラスは `ApplicationAdapter` から継承します。 `ApplicationAdapter`は`ApplicationListener`インタフェースの空の実装を提供するLibGDXクラスです。 「ApplicationListener」は、ゲームをレンダリングして更新する方法だけでなく、ゲームを初期化して破棄する方法を含むインターフェースです。

ゲームを初期化するには、 `create()` メソッドをオーバーライドする必要があります。 `create()` メソッドは、ゲームが最初に作成されたときに呼び出されます。

```kotlin
override fun create() {
}
```

`create()` メソッドから `SpriteBatch` を生成します。 `SpriteBatch`は2Dテクスチャを描くために使用されます。また、「Texture」と「Sprite」も生成します。 「テクスチャ」はプレイヤーのイメージになります。 `Sprite`は画面に `Texture`を描画するために使用されます。

```kotlin
val batch = SpriteBatch()
val texture = Texture("player.png")
val sprite = Sprite(texture)
```

また、`render()` メソッドをオーバーライドする必要があります。 `render()` メソッドはすべてのフレームで呼び出されます。 `render()` メソッドから画面を消去して `Sprite` を描きます。

```kotlin
override fun render() {
    Gdx.gl.glClearColor(1f, 1f, 1f, 1f)
    Gdx.gl.glClear(GL20.GL_COLOR_BUFFER_BIT)
    batch.begin()
    batch.draw(sprite, 0f, 0f)
    batch.end()
}
```

また、 `dispose()` メソッドをオーバーライドする必要があります。 `dispose()` メソッドは、ゲームが破壊されると呼び出されます。 `dispose()` メソッドで `SpriteBatch` と `Texture` を処理します。

```kotlin
override fun dispose() {
    batch.dispose()
    texture.dispose()
}
```

これで `Game` クラスがあるので、ゲームを開始するために `main()` 関数を作成しなければなりません。 `LwjglApplicationConfiguration`を作成し、それを使ってゲームを構築します。次に、GameクラスとLwjglApplicationConfigurationを引数として渡してLwjglApplicationを作成します。

```kotlin
fun main(args: Array<String>) {
    val config = LwjglApplicationConfiguration()
    LwjglApplication(Game(), config)
}
```

これでゲームが設定されているので、いくつかの機能を追加してみましょう。

## 機能の追加

まず、プレイヤーを左右に移動する機能を追加します。 `Game`クラスに`velocity`属性を追加してこれを行います。 `velocity`属性はプレイヤーの速度を保存するために使用されます。また、Gameクラスにupdate（）メソッドを追加します。 `update()` メソッドはすべてのフレームで呼び出されます。 `update()` メソッドでプレイヤーの速度に応じてプレイヤーの位置を更新します。

```kotlin
class Game : ApplicationAdapter() {

    private val velocity = Vector2()

    override fun update() {
        sprite.x += velocity.x * Gdx.graphics.deltaTime
        sprite.y += velocity.y * Gdx.graphics.deltaTime
    }
}
```

次に、プレイヤーがジャンプできる機能を追加します。 `Game`クラスに`jump（）`メソッドを追加してこれを行います。プレイヤーがジャンプボタンを押すと、`jump（）`メソッドが呼び出されます。 `jump()` メソッドでプレイヤーがジャンプするように速度を設定します。

```kotlin
class Game : ApplicationAdapter() {

    private val velocity = Vector2()

    fun jump() {
        velocity.y = 10f
    }

    override fun update() {
        sprite.x += velocity.x * Gdx.graphics.deltaTime
        sprite.y += velocity.y * Gdx.graphics.deltaTime
    }
}
```

これで、プレーヤーが左右に移動できる機能を追加する必要があります。 `Game`クラスに `InputProcessor`を追加してこれを行います。 `InputProcessor`は入力イベントを処理するために使用されます。 `processEvent()` メソッドで `TouchEvent.TOUCH_DOWN` イベントを確認します。イベントが `TouchEvent.TOUCH_DOWN`の場合、プレーヤーの速度を設定します。

```kotlin
class Game : ApplicationAdapter(), InputProcessor {

    private val velocity = Vector2()

    override fun processEvent(event: Event) {
        if(event is TouchEvent && event.type == TouchEvent.TOUCH_DOWN) {
            velocity.x = 10f
        }
    }

    override fun update() {
        sprite.x += velocity.x * Gdx.graphics.deltaTime
        sprite.y += velocity.y * Gdx.graphics.deltaTime
    }
}
```

これで、プレイヤーが発射体を撃つことができる機能を追加する必要があります。 `Game`クラスに`shoot（）`メソッドを追加してこれを行います。 `shoot()` メソッドは、プレイヤーがシュートボタンを押すと呼び出されます。 `shoot()` メソッドで `Bullet` を作成して `List` に追加します。

```kotlin
class Game : ApplicationAdapter() {

    private val velocity = Vector2()
    private val bullets = mutableListOf<Bullet>()

    fun shoot() {
        val bullet = Bullet()
        bullets.add(bullet)
    }

    override fun update() {
        sprite.x += velocity.x * Gdx.graphics.deltaTime
        sprite.y += velocity.y * Gdx.graphics.deltaTime

        bullets.forEach { bullet ->
            bullet.update()
        }
    }
}
```

また、Bulletクラスを作成する必要があります。 'Bullet'クラスは、箇条書きを表すために使用されます。 `Bullet`クラスに`position`属性を追加します。 `position`属性は、箇条書きの位置を格納するために使用されます。また、Bulletクラスにupdate（）メソッドを追加します。 `update()` メソッドは、弾丸の位置を更新するために使用されます。

```kotlin
class Bullet {

    val position = Vector2()

    fun update() {
        position.x += 10f
    }
}
```

これで、箇条書きをレンダリングする機能を追加する必要があります。 `Game` クラスに `render()` メソッドを追加してこれを行います。 `render()` メソッドで `Bullet` オブジェクトの `List` を繰り返し、それぞれをレンダリングします。

```kotlin
class Game : ApplicationAdapter() {

    private val velocity = Vector2()
    private val bullets = mutableListOf<Bullet>()

    fun shoot() {
        val bullet = Bullet()
        bullets.add(bullet)
    }

    override fun render() {
        Gdx.gl.glClearColor(1f, 1f, 1f, 1f)
        Gdx.gl.glClear(GL20.GL_COLOR_BUFFER_BIT)
        batch.begin()
        sprite.draw(batch)
        bullets.forEach { bullet ->
            bullet.render(batch)
        }
        batch.end()
    }
}
```

また、Bulletクラスにrender（）メソッドを追加する必要があります。 `render()` メソッドで弾丸を画面に描画します。

```kotlin
class Bullet {

    val position = Vector2()

    fun update() {
        position.x += 10f
    }

    fun render(batch: SpriteBatch) {
        batch.draw(texture, position.x, position.y)
    }
}
```

これで、弾丸を処理する機能を追加する必要があります。 `Game`クラスに`dispose（）`メソッドを追加してこれを行います。 `dispose()` メソッドで `Bullet` オブジェクトの `List` を繰り返し、それぞれに対して `dispose()` メソッドを呼び出します。

```kotlin
class Game : ApplicationAdapter() {

    private val velocity = Vector2()
    private val bullets = mutableListOf<Bullet>()

    fun shoot() {
        val bullet = Bullet()
        bullets.add(bullet)
    }

    override fun dispose() {
        batch.dispose()
        texture.dispose()
        bullets.forEach { bullet ->
            bullet.dispose()
        }
    }
}
```

また、Bulletクラスにdispose（）メソッドを追加する必要があります。 `dispose()` メソッドで箇条書きの `Texture` を処理します。

```kotlin
class Bullet {

    val position = Vector2()
    val texture = Texture("bullet.png")

    fun update() {
        position.x += 10f
    }

    fun render(batch: SpriteBatch) {
        batch.draw(texture, position.x, position.y)
    }

    fun dispose() {
        texture.dispose()
    }
}
```

これで、入力イベントを処理する機能を追加する必要があります。 `Game`クラスに `InputProcessor`を追加してこれを行います。 `processEvent()` メソッドで `TouchEvent.TOUCH_DOWN` イベントを確認します。イベントが `TouchEvent.TOUCH_DOWN` の場合、 `shoot()` メソッドを呼び出します。

```kotlin
class Game : ApplicationAdapter(), InputProcessor {

    private val velocity = Vector2()
    private val bullets = mutableListOf<Bullet>()

    override fun processEvent(event: Event) {
        if(event is TouchEvent && event.type == TouchEvent.TOUCH_DOWN) {
            shoot()
        }
    }

    fun shoot() {
        val bullet = Bullet()
        bullets.add(bullet)
    }

    override fun update() {
        sprite.x += velocity.x * Gdx.graphics.deltaTime
        sprite.y += velocity.y * Gdx.graphics.deltaTime

        bullets.forEach { bullet ->
            bullet.update()
        }
    }

    override fun render() {
        Gdx.gl.glClearColor(1f, 1f, 1f, 1f)
        Gdx.gl.glClear(GL20.GL_COLOR_BUFFER_BIT)
        batch.begin()
        sprite.draw(batch)
        bullets.forEach { bullet ->
            bullet.render(batch)
        }
        batch.end()
    }

    override fun dispose() {
        batch.dispose()
        texture.dispose()
        bullets.forEach { bullet ->
            bullet.dispose()
        }
    }
}
```

これで、入力イベントを処理する機能を追加する必要があります。 `Game`クラスに `InputProcessor`を追加してこれを行います。 `processEvent()` メソッドで `KeyEvent.KEY_PRESSED` イベントを確認します。イベントが `KeyEvent.KEY_PRESSED` の場合、 `Input.Keys.LEFT` または `Input.Keys.RIGHT` キーを確認します。 「LEFT」キーを押すと、左に移動するようにプレーヤーの速度を設定します。 「RIGHT」キーを押すと、プレーヤーの速度が右に移動するように設定されます。

```kotlin
class Game : ApplicationAdapter(), InputProcessor {

    private val velocity = Vector2()
    private val bullets = mutableListOf<Bullet>()

    override fun processEvent(event: Event) {
        if(event is TouchEvent && event.type == TouchEvent.TOUCH_DOWN) {
            shoot()
        } else if(event is KeyEvent && event.type == KeyEvent.KEY_PRESSED) {
            when(event.keyCode){
                Input.Keys.LEFT -> velocity.x = -10f
                Input.Keys.RIGHT -> velocity.x = 10f
            }
        }
    }

    fun shoot() {
        val bullet = Bullet()
        bullets.add(bullet)
    }

    override fun update() {
        sprite.x += velocity.x * Gdx.graphics.deltaTime
        sprite.y += velocity.y * Gdx.graphics.deltaTime

        bullets.forEach { bullet ->
            bullet.update()
        }
    }

    override fun render() {
        Gdx.gl.glClearColor(1f, 1f, 1f, 1f)
        Gdx.gl.glClear(GL20.GL_COLOR_BUFFER_BIT)
        batch.begin()
        sprite.draw(batch)
        bullets.forEach { bullet ->
            bullet.render(batch)
        }
        batch.end()
    }

    override fun dispose() {
        batch.dispose()
        texture.dispose()
        bullets.forEach { bullet ->
            bullet.dispose()
        }
    }
}
```

これで、入力イベントを処理する機能を追加する必要があります。私たち