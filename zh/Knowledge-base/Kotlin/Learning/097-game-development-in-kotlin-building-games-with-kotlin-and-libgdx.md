---
title: 097：Kotlin 游戏开发：使用 Kotlin 和 LibGDX 构建游戏
description: 
published: true
date: 2023-01-31T20:38:18.497Z
tags: 
editor: markdown
dateCreated: 2023-01-31T20:38:16.829Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [097: Game Development in Kotlin: Building Games with Kotlin and LibGDX***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/097-game-development-in-kotlin-building-games-with-kotlin-and-libgdx)
{.links-list}


# 097：Kotlin 游戏开发：使用 Kotlin 和 LibGDX 构建游戏

Kotlin 是一种 JVM 语言，因其简洁的语法和与 Java 的互操作性而越来越受欢迎。在本文中，我们将探讨如何使用 Kotlin 通过 LibGDX 库进行游戏开发。

LibGDX 是一个跨平台游戏开发库，提供跨多个平台的统一 API。它支持 Android、iOS、桌面和 HTML5。 LibGDX 应用程序是用 Java 编写的，但我们可以使用 Kotlin 代替 GDX-Kotlin 包装器库。

GDX-Kotlin 是 LibGDX 的 Kotlin 包装器。它为 LibGDX 提供 Kotlin 扩展和实用程序。 GDX-Kotlin 使得将 Kotlin 与 LibGDX 一起使用变得容易。

要将 Kotlin 与 LibGDX 一起使用，我们需要将 GDX-Kotlin 库添加到我们的项目中。我们可以通过将以下内容添加到我们的 build.gradle 文件中来使用 Gradle 做到这一点：

```groovy
repositories {
    mavenCentral()
}

dependencies {
    implementation "org.jetbrains.kotlin:kotlin-stdlib:$kotlin_version"
    implementation "org.jetbrains.kotlin:kotlin-reflect:$kotlin_version"
    implementation "com.badlogicgames.gdx:gdx-kotlin:$gdx_version"
}
```

我们还需要将 Kotlin 插件添加到我们的项目中。我们可以通过将以下内容添加到我们的 build.gradle 文件中来做到这一点：

```groovy
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

现在我们已经设置了项目，让我们使用 LibGDX 在 Kotlin 中编写一个简单的游戏。

## 一个简单的游戏

我们将从使用 LibGDX 在 Kotlin 中编写一个简单的游戏开始。我们的游戏将是一款 2D 平台游戏。玩家将能够左右移动、跳跃和发射弹丸。

我们将从为我们的游戏定义一个类开始。我们将我们的班级称为“游戏”。

```kotlin
class Game : ApplicationAdapter() {
}
```

我们的 `Game` 类继承自 `ApplicationAdapter`。 `ApplicationAdapter` 是一个 LibGDX 类，它提供 `ApplicationListener` 接口的空实现。 `ApplicationListener` 是一个接口，包含初始化和部署游戏的方法，以及渲染和更新游戏的方法。

我们需要覆盖 `create()` 方法来初始化我们的游戏。首次创建游戏时会调用 create() 方法。

```kotlin
override fun create() {
}
```

在 `create()` 方法中，我们将创建一个 `SpriteBatch`。 `SpriteBatch` 用于绘制 2D 纹理。我们还将创建一个 `Texture` 和一个 `Sprite`。 `Texture` 将是我们播放器的图像。 `Sprite` 将用于将 `Texture` 绘制到屏幕上。

```kotlin
val batch = SpriteBatch()
val texture = Texture("player.png")
val sprite = Sprite(texture)
```

我们还需要覆盖 `render()` 方法。 `render()` 方法在每一帧上被调用。在 `render()` 方法中，我们将清除屏幕并绘制我们的 `Sprite`。

```kotlin
override fun render() {
    Gdx.gl.glClearColor(1f, 1f, 1f, 1f)
    Gdx.gl.glClear(GL20.GL_COLOR_BUFFER_BIT)
    batch.begin()
    batch.draw(sprite, 0f, 0f)
    batch.end()
}
```

我们还需要覆盖 `dispose()` 方法。销毁游戏时调用 `dispose()` 方法。在 `dispose()` 方法中，我们将处理我们的 `SpriteBatch` 和 `Texture`。

```kotlin
override fun dispose() {
    batch.dispose()
    texture.dispose()
}
```

现在我们有了 `Game` 类，我们需要创建一个 `main()` 函数来启动我们的游戏。我们将创建一个 LwjglApplicationConfiguration 并使用它来配置我们的游戏。然后我们将创建一个 `LwjglApplication`，传入我们的 `Game` 类和 `LwjglApplicationConfiguration` 作为参数。

```kotlin
fun main(args: Array<String>) {
    val config = LwjglApplicationConfiguration()
    LwjglApplication(Game(), config)
}
```

现在我们已经设置了游戏，让我们向它添加一些功能。

## 添加功能

首先，我们将添加左右移动玩家的功能。我们将通过向我们的 Game 类添加一个 velocity 属性来做到这一点。 `velocity` 属性将用于存储玩家的速度。我们还将向我们的 Game 类添加一个 update() 方法。将在每一帧调用 `update()` 方法。在 update() 方法中，我们将根据玩家的速度更新玩家的位置。

```kotlin
class Game : ApplicationAdapter() {

    private val velocity = Vector2()

    override fun update() {
        sprite.x += velocity.x * Gdx.graphics.deltaTime
        sprite.y += velocity.y * Gdx.graphics.deltaTime
    }
}
```

接下来，我们将为玩家添加跳跃的能力。我们将通过向我们的 Game 类添加一个 jump() 方法来做到这一点。当玩家按下跳跃按钮时，将调用 jump() 方法。在 `jump()` 方法中，我们将设置玩家的速度以使他们跳跃。

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

现在，我们需要为玩家添加左右移动的能力。我们将通过向我们的 Game 类添加一个 InputProcessor 来做到这一点。 `InputProcessor` 将用于处理输入事件。在 `processEvent()` 方法中，我们将检查 `TouchEvent.TOUCH_DOWN` 事件。如果事件是“TouchEvent.TOUCH_DOWN”，我们将设置玩家的速度。

```kotlin
class Game : ApplicationAdapter(), InputProcessor {

    private val velocity = Vector2()

    override fun processEvent(event: Event) {
        if (event is TouchEvent && event.type == TouchEvent.TOUCH_DOWN) {
            velocity.x = 10f
        }
    }

    override fun update() {
        sprite.x += velocity.x * Gdx.graphics.deltaTime
        sprite.y += velocity.y * Gdx.graphics.deltaTime
    }
}
```

现在，我们需要为玩家添加发射弹丸的能力。我们将通过向我们的 Game 类添加一个 shoot() 方法来做到这一点。当玩家按下射击按钮时，将调用 `shoot()` 方法。在 `shoot()` 方法中，我们将创建一个 `Bullet` 并将其添加到 `List` 中。

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

我们还需要创建一个“Bullet”类。 `Bullet` 类将用于表示子弹。我们将向 `Bullet` 类添加一个 `position` 属性。 `position` 属性将用于存储子弹的位置。我们还将向 `Bullet` 类添加 `update()` 方法。 `update()` 方法将用于更新项目符号的位置。

```kotlin
class Bullet {

    val position = Vector2()

    fun update() {
        position.x += 10f
    }
}
```

现在，我们需要添加渲染子弹的功能。我们将通过向我们的 Game 类添加一个 render() 方法来做到这一点。在 `render()` 方法中，我们将遍历 `Bullet` 对象的 `List` 并渲染每一个。

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

我们还需要向我们的 Bullet 类添加一个 render() 方法。在 `render()` 方法中，我们将把子弹绘制到屏幕上。

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

现在，我们需要添加处理子弹的功能。我们将通过向我们的 Game 类添加一个 dispose() 方法来做到这一点。在 `dispose()` 方法中，我们将遍历 `Bullet` 对象的 `List` 并在每个对象上调用 `dispose()` 方法。

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

我们还需要向我们的 Bullet 类添加一个 dispose() 方法。在 `dispose()` 方法中，我们将处理子弹的 `Texture`。

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

现在，我们需要添加处理输入事件的能力。我们将通过向我们的 Game 类添加一个 InputProcessor 来做到这一点。在 `processEvent()` 方法中，我们将检查 `TouchEvent.TOUCH_DOWN` 事件。如果事件是“TouchEvent.TOUCH_DOWN”，我们将调用“shoot()”方法。

```kotlin
class Game : ApplicationAdapter(), InputProcessor {

    private val velocity = Vector2()
    private val bullets = mutableListOf<Bullet>()

    override fun processEvent(event: Event) {
        if (event is TouchEvent && event.type == TouchEvent.TOUCH_DOWN) {
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

现在，我们需要添加处理输入事件的能力。我们将通过向我们的 Game 类添加一个 InputProcessor 来做到这一点。在 `processEvent()` 方法中，我们将检查 `KeyEvent.KEY_PRESSED` 事件。如果事件是“KeyEvent.KEY_PRESSED”，我们将检查“Input.Keys.LEFT”或“Input.Keys.RIGHT”键。如果按下“LEFT”键，我们会将玩家的速度设置为向左移动。如果按下“RIGHT”键，我们会将玩家的速度设置为向右移动。

```kotlin
class Game : ApplicationAdapter(), InputProcessor {

    private val velocity = Vector2()
    private val bullets = mutableListOf<Bullet>()

    override fun processEvent(event: Event) {
        if (event is TouchEvent && event.type == TouchEvent.TOUCH_DOWN) {
            shoot()
        } else if (event is KeyEvent && event.type == KeyEvent.KEY_PRESSED) {
            when (event.keyCode) {
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

现在，我们需要添加处理输入事件的能力。我们