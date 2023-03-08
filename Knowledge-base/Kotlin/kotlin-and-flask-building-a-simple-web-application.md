---
title: Kotlin 및 Flask: 간단한 웹 애플리케이션 구축
description: 
published: true
date: 2023-02-01T05:36:31.958Z
tags: 
editor: markdown
dateCreated: 2023-02-01T05:36:30.337Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Kotlin and Flask: Building a Simple Web Application***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-flask-building-a-simple-web-application)
{.links-list}



# Kotlin과 Flask: 간단한 웹 애플리케이션 구축

Kotlin은 JVM에서 실행되는 정적으로 유형이 지정된 프로그래밍 언어이며 JavaScript 또는 네이티브 코드로 컴파일할 수도 있습니다. 함수형 프로그래밍과 객체 지향 프로그래밍의 기능을 결합한 실용적인 오픈 소스 언어입니다.

Flask는 작은 코어와 확장하기 쉬운 철학으로 구축된 Python 웹 프레임워크입니다. Flask는 가벼운 특성으로 인해 마이크로서비스 구축에 널리 사용됩니다.

이 기사에서는 Kotlin과 Flask를 사용하여 간단한 웹 애플리케이션을 빌드하는 방법을 알아봅니다. 먼저 개발 환경을 설정한 다음 Kotlin 클래스와 Flask 경로를 만들어 간단한 메시지를 표시합니다.

## 개발 환경 설정

코딩을 시작하기 전에 개발 환경을 설정해야 합니다. Kotlin 컴파일러와 Flask 웹 프레임워크를 설치해야 합니다.

### Kotlin 컴파일러 설치

Kotlin 컴파일러는 [공식 Kotlin 웹사이트](https://kotlinlang.org/)에서 설치할 수 있습니다. Windows, macOS 및 Linux에 Kotlin을 설치하기 위한 지침이 있습니다.

### 플라스크 설치

Flask는 [pip](https://pip.pypa.io/en/stable/) 패키지 관리자를 사용하여 [Python Package Index](https://pypi.org/)에서 설치할 수 있습니다.

```
$ pip install flask
```

## 안녕, 코틀린

이제 개발 환경이 설정되었으므로 Kotlin 코드를 작성해 보겠습니다. `Hello.kt`라는 Kotlin 파일을 만드는 것으로 시작하겠습니다.

```kotlin
fun main(args: Array<String>) {
    println("Hello, Kotlin!")
}
```

`kotlinc` 컴파일러를 사용하여 이 Kotlin 코드를 JavaScript로 컴파일할 수 있습니다.

```
$ kotlinc Hello.kt -output hello.js
```

`kotlinc-native` 컴파일러를 사용하여 네이티브 코드로 컴파일할 수도 있습니다.

```
$ kotlinc-native Hello.kt -o hello
```

## 안녕, 플라스크

이제 Kotlin 파일이 있으므로 간단한 메시지를 표시하는 Flask 경로를 작성해 보겠습니다. `app.py`라는 파일을 만들고 `Flask` 클래스를 가져옵니다.

```python
from flask import Flask
```

다음으로 `Flask` 클래스의 인스턴스를 만듭니다. 애플리케이션의 이름을 전달해야 합니다.

```python
app = Flask(__name__)
```

이제 경로를 만들 수 있습니다. 경로는 `@app.route` 데코레이터로 장식된 함수입니다. `@app.route` 데코레이터는 경로를 인수로 사용합니다. 함수와 연결될 경로입니다.

```python
@app.route('/')
def index():
    return 'Hello, Flask!'
```

마지막으로 Flask에게 애플리케이션을 실행하도록 지시해야 합니다. 우리는 `run` 메서드를 호출하여 이를 수행합니다.

```python
if __name__ == '__main__':
    app.run()
```

Flask 명령을 사용하여 Flask 애플리케이션을 실행할 수 있습니다.

```
$ flask run
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C to quit)
```

이제 http://127.0.0.1:5000/에서 애플리케이션에 액세스할 수 있습니다.

## 결론

이 기사에서는 Kotlin과 Flask를 사용하여 간단한 웹 애플리케이션을 빌드하는 방법을 살펴보았습니다. 개발 환경을 설정하는 것으로 시작한 다음 Kotlin 파일과 Flask 경로를 만들어 간단한 메시지를 표시했습니다.