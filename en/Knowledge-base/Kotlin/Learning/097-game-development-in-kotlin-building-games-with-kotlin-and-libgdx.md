---
title: 097: Game Development in Kotlin: Building Games with Kotlin and LibGDX
description: 
published: true
date: 2023-01-31T20:38:20.531Z
tags: 
editor: markdown
dateCreated: 2023-01-31T20:38:16.819Z
---

- [097: Kotlin으로 게임 개발: Kotlin과 LibGDX로 게임 만들기***Korean** version of this document is available*](/ko/Knowledge-base/Kotlin/Learning/097-game-development-in-kotlin-building-games-with-kotlin-and-libgdx)
{.links-list}
- [097: Kotlin でのゲーム開発: Kotlin と LibGDX を使用したゲームのビルド***Japanese** version of this document is available*](/ja/Knowledge-base/Kotlin/Learning/097-game-development-in-kotlin-building-games-with-kotlin-and-libgdx)
{.links-list}
- [097：Kotlin 游戏开发：使用 Kotlin 和 LibGDX 构建游戏***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/Kotlin/Learning/097-game-development-in-kotlin-building-games-with-kotlin-and-libgdx)
{.links-list}


# 097: Game Development in Kotlin: Building Games with Kotlin and LibGDX

Kotlin is a JVM language that is gaining popularity for its concise syntax and interoperability with Java. In this article, we'll explore how to use Kotlin for game development with the LibGDX library.

LibGDX is a cross-platform game development library that provides a unified API across multiple platforms. It supports Android, iOS, Desktop, and HTML5. LibGDX applications are written in Java, but we can use Kotlin instead with the GDX-Kotlin wrapper library.

GDX-Kotlin is a Kotlin wrapper for LibGDX. It provides Kotlin extensions and utilities for LibGDX. GDX-Kotlin makes it easy to use Kotlin with LibGDX.

To use Kotlin with LibGDX, we need to add the GDX-Kotlin library to our project. We can do this with Gradle by adding the following to our build.gradle file:

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

We also need to add the Kotlin plugin to our project. We can do this by adding the following to our build.gradle file:

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

Now that we have our project set up, let's write a simple game in Kotlin with LibGDX.

## A Simple Game

We'll start by writing a simple game in Kotlin with LibGDX. Our game will be a 2D platformer. The player will be able to move left and right, jump, and shoot projectiles.

We'll start by defining a class for our game. We'll call our class `Game`.

```kotlin
class Game : ApplicationAdapter() {
}
```

Our `Game` class inherits from `ApplicationAdapter`. `ApplicationAdapter` is a LibGDX class that provides empty implementations of the `ApplicationListener` interface. `ApplicationListener` is an interface that contains methods for initializing and disposing a game, as well as methods for rendering and updating a game.

We need to override the `create()` method to initialize our game. The `create()` method is called when the game is first created.

```kotlin
override fun create() {
}
```

In the `create()` method, we'll create a `SpriteBatch`. A `SpriteBatch` is used to draw 2D textures. We'll also create a `Texture` and a `Sprite`. The `Texture` will be the image for our player. The `Sprite` will be used to draw the `Texture` to the screen.

```kotlin
val batch = SpriteBatch()
val texture = Texture("player.png")
val sprite = Sprite(texture)
```

We also need to override the `render()` method. The `render()` method is called on every frame. In the `render()` method, we'll clear the screen and draw our `Sprite`.

```kotlin
override fun render() {
    Gdx.gl.glClearColor(1f, 1f, 1f, 1f)
    Gdx.gl.glClear(GL20.GL_COLOR_BUFFER_BIT)
    batch.begin()
    batch.draw(sprite, 0f, 0f)
    batch.end()
}
```

We also need to override the `dispose()` method. The `dispose()` method is called when the game is destroyed. In the `dispose()` method, we'll dispose of our `SpriteBatch` and `Texture`.

```kotlin
override fun dispose() {
    batch.dispose()
    texture.dispose()
}
```

Now that we have our `Game` class, we need to create a `main()` function to launch our game. We'll create a `LwjglApplicationConfiguration` and use it to configure our game. We'll then create a `LwjglApplication`, passing in our `Game` class and the `LwjglApplicationConfiguration` as arguments.

```kotlin
fun main(args: Array<String>) {
    val config = LwjglApplicationConfiguration()
    LwjglApplication(Game(), config)
}
```

Now that we have our game set up, let's add some functionality to it.

## Adding Functionality

First, we'll add the ability to move our player left and right. We'll do this by adding a `velocity` property to our `Game` class. The `velocity` property will be used to store the player's velocity. We'll also add an `update()` method to our `Game` class. The `update()` method will be called on every frame. In the `update()` method, we'll update the player's position based on their velocity.

```kotlin
class Game : ApplicationAdapter() {

    private val velocity = Vector2()

    override fun update() {
        sprite.x += velocity.x * Gdx.graphics.deltaTime
        sprite.y += velocity.y * Gdx.graphics.deltaTime
    }
}
```

Next, we'll add the ability for the player to jump. We'll do this by adding a `jump()` method to our `Game` class. The `jump()` method will be called when the player presses the jump button. In the `jump()` method, we'll set the player's velocity to make them jump.

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

Now, we need to add the ability for the player to move left and right. We'll do this by adding an `InputProcessor` to our `Game` class. The `InputProcessor` will be used to process input events. In the `processEvent()` method, we'll check for the `TouchEvent.TOUCH_DOWN` event. If the event is `TouchEvent.TOUCH_DOWN`, we'll set the player's velocity.

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

Now, we need to add the ability for the player to shoot projectiles. We'll do this by adding a `shoot()` method to our `Game` class. The `shoot()` method will be called when the player presses the shoot button. In the `shoot()` method, we'll create a `Bullet` and add it to a `List`.

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

We also need to create a `Bullet` class. The `Bullet` class will be used to represent bullets. We'll add a `position` property to the `Bullet` class. The `position` property will be used to store the bullet's position. We'll also add an `update()` method to the `Bullet` class. The `update()` method will be used to update the bullet's position.

```kotlin
class Bullet {

    val position = Vector2()

    fun update() {
        position.x += 10f
    }
}
```

Now, we need to add the ability to render our bullets. We'll do this by adding a `render()` method to our `Game` class. In the `render()` method, we'll iterate over our `List` of `Bullet` objects and render each one.

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

We also need to add a `render()` method to our `Bullet` class. In the `render()` method, we'll draw the bullet to the screen.

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

Now, we need to add the ability to dispose of our bullets. We'll do this by adding a `dispose()` method to our `Game` class. In the `dispose()` method, we'll iterate over our `List` of `Bullet` objects and call the `dispose()` method on each one.

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

We also need to add a `dispose()` method to our `Bullet` class. In the `dispose()` method, we'll dispose of the bullet's `Texture`.

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

Now, we need to add the ability to process input events. We'll do this by adding an `InputProcessor` to our `Game` class. In the `processEvent()` method, we'll check for the `TouchEvent.TOUCH_DOWN` event. If the event is `TouchEvent.TOUCH_DOWN`, we'll call the `shoot()` method.

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

Now, we need to add the ability to process input events. We'll do this by adding an `InputProcessor` to our `Game` class. In the `processEvent()` method, we'll check for the `KeyEvent.KEY_PRESSED` event. If the event is `KeyEvent.KEY_PRESSED`, we'll check for the `Input.Keys.LEFT` or `Input.Keys.RIGHT` key. If the `LEFT` key is pressed, we'll set the player's velocity to move left. If the `RIGHT` key is pressed, we'll set the player's velocity to move right.

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

Now, we need to add the ability to process input events. We