---
title: 097: Kotlin으로 게임 개발: Kotlin과 LibGDX로 게임 만들기
description: 
published: true
date: 2023-01-31T20:38:18.517Z
tags: 
editor: markdown
dateCreated: 2023-01-31T20:38:16.821Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [097: Game Development in Kotlin: Building Games with Kotlin and LibGDX***English** version of this document is available*](/en/Knowledge-base/Kotlin/Learning/097-game-development-in-kotlin-building-games-with-kotlin-and-libgdx)
{.links-list}


# 097: Kotlin으로 게임 개발: Kotlin과 LibGDX로 게임 만들기

Kotlin은 간결한 구문과 Java와의 상호 운용성으로 인기를 얻고 있는 JVM 언어입니다. 이 기사에서는 LibGDX 라이브러리로 게임 개발에 Kotlin을 사용하는 방법을 살펴보겠습니다.

LibGDX는 여러 플랫폼에서 통합 API를 제공하는 크로스 플랫폼 게임 개발 라이브러리입니다. Android, iOS, 데스크톱 및 HTML5를 지원합니다. LibGDX 애플리케이션은 Java로 작성되지만 GDX-Kotlin 래퍼 라이브러리 대신 Kotlin을 사용할 수 있습니다.

GDX-Kotlin은 LibGDX용 Kotlin 래퍼입니다. LibGDX용 Kotlin 확장 및 유틸리티를 제공합니다. GDX-Kotlin을 사용하면 LibGDX와 함께 Kotlin을 쉽게 사용할 수 있습니다.

LibGDX와 함께 Kotlin을 사용하려면 프로젝트에 GDX-Kotlin 라이브러리를 추가해야 합니다. build.gradle 파일에 다음을 추가하여 Gradle로 이 작업을 수행할 수 있습니다.

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

또한 프로젝트에 Kotlin 플러그인을 추가해야 합니다. build.gradle 파일에 다음을 추가하면 됩니다.

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

이제 프로젝트가 설정되었으므로 LibGDX를 사용하여 Kotlin으로 간단한 게임을 작성해 보겠습니다.

## 간단한 게임

LibGDX를 사용하여 Kotlin으로 간단한 게임을 작성하는 것으로 시작하겠습니다. 우리 게임은 2D 플랫포머가 될 것입니다. 플레이어는 좌우로 움직이고, 점프하고, 발사체를 쏠 수 있습니다.

게임의 클래스를 정의하는 것으로 시작하겠습니다. 클래스를 `Game`이라고 부를 것입니다.

```kotlin
class Game : ApplicationAdapter() {
}
```

우리의 `Game` 클래스는 `ApplicationAdapter`에서 상속받습니다. `ApplicationAdapter`는 `ApplicationListener` 인터페이스의 빈 구현을 제공하는 LibGDX 클래스입니다. 'ApplicationListener'는 게임을 렌더링하고 업데이트하는 방법뿐만 아니라 게임을 초기화하고 폐기하는 방법을 포함하는 인터페이스입니다.

게임을 초기화하려면 `create()` 메서드를 재정의해야 합니다. `create()` 메서드는 게임이 처음 생성될 때 호출됩니다.

```kotlin
override fun create() {
}
```

`create()` 메소드에서 `SpriteBatch`를 생성합니다. `SpriteBatch`는 2D 텍스처를 그리는 데 사용됩니다. 또한 `Texture`와 `Sprite`도 생성합니다. `텍스처`는 플레이어의 이미지가 됩니다. `Sprite`는 화면에 `Texture`를 그리는 데 사용됩니다.

```kotlin
val batch = SpriteBatch()
val texture = Texture("player.png")
val sprite = Sprite(texture)
```

또한 `render()` 메서드를 재정의해야 합니다. `render()` 메서드는 모든 프레임에서 호출됩니다. `render()` 메서드에서 화면을 지우고 `Sprite`를 그립니다.

```kotlin
override fun render() {
    Gdx.gl.glClearColor(1f, 1f, 1f, 1f)
    Gdx.gl.glClear(GL20.GL_COLOR_BUFFER_BIT)
    batch.begin()
    batch.draw(sprite, 0f, 0f)
    batch.end()
}
```

또한 `dispose()` 메서드를 재정의해야 합니다. `dispose()` 메서드는 게임이 파괴될 때 호출됩니다. `dispose()` 메서드에서 `SpriteBatch` 및 `Texture`를 처리합니다.

```kotlin
override fun dispose() {
    batch.dispose()
    texture.dispose()
}
```

이제 `Game` 클래스가 있으므로 게임을 시작하기 위해 `main()` 함수를 만들어야 합니다. `LwjglApplicationConfiguration`을 생성하고 이를 사용하여 게임을 구성합니다. 그런 다음 `Game` 클래스와 `LwjglApplicationConfiguration`을 인수로 전달하여 `LwjglApplication`을 만듭니다.

```kotlin
fun main(args: Array<String>) {
    val config = LwjglApplicationConfiguration()
    LwjglApplication(Game(), config)
}
```

이제 게임이 설정되었으므로 몇 가지 기능을 추가해 보겠습니다.

## 기능 추가

먼저 플레이어를 좌우로 이동하는 기능을 추가합니다. `Game` 클래스에 `velocity` 속성을 추가하여 이를 수행합니다. `velocity` 속성은 플레이어의 속도를 저장하는 데 사용됩니다. 또한 `Game` 클래스에 `update()` 메서드를 추가합니다. `update()` 메서드는 모든 프레임에서 호출됩니다. `update()` 메서드에서 플레이어의 속도에 따라 플레이어의 위치를 업데이트합니다.

```kotlin
class Game : ApplicationAdapter() {

    private val velocity = Vector2()

    override fun update() {
        sprite.x += velocity.x * Gdx.graphics.deltaTime
        sprite.y += velocity.y * Gdx.graphics.deltaTime
    }
}
```

다음으로 플레이어가 점프할 수 있는 기능을 추가합니다. `Game` 클래스에 `jump()` 메서드를 추가하여 이를 수행합니다. 플레이어가 점프 버튼을 누르면 `jump()` 메서드가 호출됩니다. `jump()` 메서드에서 플레이어가 점프하도록 속도를 설정합니다.

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

이제 플레이어가 좌우로 이동할 수 있는 기능을 추가해야 합니다. `Game` 클래스에 `InputProcessor`를 추가하여 이를 수행합니다. `InputProcessor`는 입력 이벤트를 처리하는 데 사용됩니다. `processEvent()` 메서드에서 `TouchEvent.TOUCH_DOWN` 이벤트를 확인합니다. 이벤트가 `TouchEvent.TOUCH_DOWN`인 경우 플레이어의 속도를 설정합니다.

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

이제 플레이어가 발사체를 쏠 수 있는 기능을 추가해야 합니다. `Game` 클래스에 `shoot()` 메서드를 추가하여 이를 수행합니다. `shoot()` 메서드는 플레이어가 슛 버튼을 누를 때 호출됩니다. `shoot()` 메서드에서 `Bullet`을 만들고 `List`에 추가합니다.

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

또한 `Bullet` 클래스를 만들어야 합니다. 'Bullet' 클래스는 글머리 기호를 나타내는 데 사용됩니다. `Bullet` 클래스에 `position` 속성을 추가합니다. `position` 속성은 글머리 기호의 위치를 저장하는 데 사용됩니다. 또한 `Bullet` 클래스에 `update()` 메서드를 추가합니다. `update()` 메서드는 총알의 위치를 업데이트하는 데 사용됩니다.

```kotlin
class Bullet {

    val position = Vector2()

    fun update() {
        position.x += 10f
    }
}
```

이제 글머리 기호를 렌더링하는 기능을 추가해야 합니다. `Game` 클래스에 `render()` 메서드를 추가하여 이를 수행합니다. `render()` 메서드에서 `Bullet` 개체의 `List`를 반복하고 각각을 렌더링합니다.

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

또한 `Bullet` 클래스에 `render()` 메서드를 추가해야 합니다. `render()` 메서드에서 총알을 화면에 그립니다.

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

이제 총알을 처리하는 기능을 추가해야 합니다. `Game` 클래스에 `dispose()` 메서드를 추가하여 이를 수행합니다. `dispose()` 메서드에서 `Bullet` 개체의 `List`를 반복하고 각각에 대해 `dispose()` 메서드를 호출합니다.

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

또한 `Bullet` 클래스에 `dispose()` 메서드를 추가해야 합니다. `dispose()` 메서드에서 글머리 기호의 `Texture`를 처리합니다.

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

이제 입력 이벤트를 처리하는 기능을 추가해야 합니다. `Game` 클래스에 `InputProcessor`를 추가하여 이를 수행합니다. `processEvent()` 메서드에서 `TouchEvent.TOUCH_DOWN` 이벤트를 확인합니다. 이벤트가 `TouchEvent.TOUCH_DOWN`인 경우 `shoot()` 메서드를 호출합니다.

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

이제 입력 이벤트를 처리하는 기능을 추가해야 합니다. `Game` 클래스에 `InputProcessor`를 추가하여 이를 수행합니다. `processEvent()` 메서드에서 `KeyEvent.KEY_PRESSED` 이벤트를 확인합니다. 이벤트가 `KeyEvent.KEY_PRESSED`인 경우 `Input.Keys.LEFT` 또는 `Input.Keys.RIGHT` 키를 확인합니다. 'LEFT' 키를 누르면 왼쪽으로 이동하도록 플레이어의 속도를 설정합니다. 'RIGHT' 키를 누르면 플레이어의 속도가 오른쪽으로 이동하도록 설정됩니다.

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

이제 입력 이벤트를 처리하는 기능을 추가해야 합니다. 우리