---
title: Python 프로그래밍: 초보자 가이드
description: 
published: true
date: 2023-02-01T14:25:08.602Z
tags: 
editor: markdown
dateCreated: 2023-02-01T14:25:07.049Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Programming with Python: A Beginner's Guide***English** version of this document is available*](/en/Knowledge-base/Common/programming-with-python-a-beginner-s-guide)
{.links-list}



# 파이썬 프로그래밍: 초보자 가이드

Python은 웹 애플리케이션의 백엔드, 프런트엔드 또는 전체 스택에서 사용할 수 있는 다재다능한 언어입니다. 이 가이드에서는 Python 프로그래밍을 시작하는 방법을 보여줍니다.

## 왜 파이썬인가?

Python은 웹 개발, 과학 컴퓨팅, 인공 지능 등에 널리 사용되는 언어입니다. 초보자가 배우기 쉽고 강력한 개발을 가능하게 하는 많은 모듈과 라이브러리가 있습니다.

## 파이썬 설치하기

Python으로 프로그래밍을 시작하기 전에 Python을 컴퓨터에 설치해야 합니다. Python은 [Python 공식 웹사이트](https://www.python.org/)에서 다운로드할 수 있습니다.

Python을 다운로드하고 설치한 후 명령줄 인터페이스를 열고 `python`을 입력하여 작동하는지 확인할 수 있습니다. Python이 설치되어 있으면 다음과 같이 표시됩니다.

```
Python 3.7.4 (default, Aug 13 2019, 15:17:50) 
[Clang 4.0.1 (tags/RELEASE_401/final)] on darwin
Type "help", "copyright", "credits" or "license" for more information.
>>> 
```

이 메시지가 표시되면 Python에서 프로그래밍을 시작할 준비가 된 것입니다. 이것이 표시되지 않으면 Python을 올바르게 설치했고 시스템 경로에 추가되었는지 확인하십시오.

## 파이썬 문법

파이썬은 높은 수준의 인터프리터 언어입니다. 이는 하드웨어 및 운영 체제의 세부 사항에서 추상화됨을 의미합니다. Python 코드는 모듈과 패키지로 구성됩니다. 모듈은 Python 코드를 포함하는 파일입니다. 패키지는 모듈의 모음입니다.

Python 코드는 인터프리터가 읽고 한 줄씩 실행됩니다. 인터프리터는 `python`을 입력하여 명령줄에서 호출할 수 있습니다. 이렇게 하면 Python 인터프리터가 대화형 모드로 열립니다. 대화식 모드에서 Python 코드를 입력하면 인터프리터가 즉시 실행합니다.

Python 인터프리터를 종료하려면 `exit()`를 입력하십시오.

Python 코드는 Python 파일에서 실행할 수도 있습니다. Python 파일은 확장자가 `.py`인 텍스트 파일입니다. Python 파일을 실행하려면 `python` 다음에 파일 경로를 입력하십시오. 예를 들어 현재 디렉토리에 `hello.py` 파일이 있으면 `python hello.py`를 입력하여 실행할 수 있습니다.

## 헬로월드!

이제 Python을 설치하고 실행하는 방법을 알았으므로 첫 번째 프로그램을 작성해 보겠습니다. 고전적인 "Hello, World!"부터 시작하겠습니다. 프로그램.

좋아하는 텍스트 편집기를 열고 `hello.py`라는 새 파일을 만듭니다. 파일에 다음 코드를 추가합니다.

```python
print("Hello, World!")
```

파일을 저장하고 텍스트 편집기를 닫습니다. 그런 다음 명령줄 인터페이스를 열고 `hello.py`가 저장된 디렉토리로 이동합니다. 프로그램을 실행하려면 `python hello.py`를 입력하십시오. 다음 출력이 표시되어야 합니다.

```
Hello, World!
```

축하합니다! 첫 번째 Python 프로그램을 작성했습니다.

## 변수

Python에서 변수는 값을 저장하는 데 사용됩니다. 값은 문자열, 숫자, 목록 또는 기타 데이터 유형이 될 수 있습니다. 변수를 생성하려면 변수의 이름과 저장할 값을 지정하기만 하면 됩니다. 예를 들어:

```python
message = "Hello, World!"
```

위의 예에서 `message`라는 변수를 만들고 그 안에 문자열 `"Hello, World!"`를 저장합니다. 그런 다음 변수 이름을 사용하여 변수 값에 액세스할 수 있습니다.

```python
print(message)
```

'Hello, World!'를 출력합니다.

변수를 재할당하여 변수 값을 변경할 수도 있습니다.

```python
message = "Hello, Python!"
```

이제 `message`를 인쇄하면 `Hello, Python!`이 표시됩니다.

설명적이고 기억하기 쉬운 변수 이름을 선택하는 것이 중요합니다. 예를 들어 `message`는 문자열을 저장하는 변수의 좋은 이름입니다. `x`라는 변수는 그 변수가 무엇을 위해 사용되는지 알려주지 않기 때문에 좋은 이름이 아닙니다.

## 데이터 유형

Python에는 몇 가지 기본 제공 데이터 유형이 있습니다.

* `int`: 정수 값. 예: `1`, `-5`, `0`.
* `float`: 부동 소수점 값. 예: `1.0`, `-5.0`, `0.0`.
* `str`: 문자열 값. 예: `"Hello, World!"`, `"Python"`.
* `bool`: 부울 값. 예: '참', '거짓'.
* `list`: 값 목록. 예: `[1, 2, 3]`, `["a", "b", "c"]`.
* `dict`: 값의 사전. 예: `{"a": 1, "b": 2, "c": 3}`.

`type()` 함수를 사용하여 값의 유형을 찾을 수 있습니다.

```python
>>> type(1)
<class 'int'>
>>> type(1.0)
<class 'float'>
>>> type("Hello, World!")
<class 'str'>
>>> type(True)
<class 'bool'>
>>> type([1, 2, 3])
<class 'list'>
>>> type({"a": 1, "b": 2, "c": 3})
<class 'dict'>
```

데이터 유형마다 속성과 기능이 다르기 때문에 값의 데이터 유형을 아는 것이 중요합니다. 예를 들어 `int` 값에는 사용할 수 있는 `abs()` 및 `pow()`와 같은 수학 함수가 있고 `str` 값에는 `upper()` 및 `lower()`와 같은 문자열 함수가 있습니다.

## 목록

목록은 단일 변수에 여러 값을 저장할 수 있는 데이터 구조 유형입니다. 대괄호 `[]` 안에 값을 넣으면 목록이 생성됩니다. 예를 들어:

```python
>>> my_list = [1, 2, 3]
>>> my_list
[1, 2, 3]
```

색인을 사용하여 목록의 값에 액세스할 수 있습니다. 인덱스는 목록에서 값의 위치를 지정하는 숫자입니다. 목록의 첫 번째 값의 인덱스는 '0'이고 두 번째 값의 인덱스는 '1'입니다. 예를 들어:

```python
>>> my_list[0]
1
>>> my_list[1]
2
>>> my_list[2]
3
```

음수 인덱스를 사용하여 목록의 끝에서 값에 액세스할 수도 있습니다. 예를 들어 색인 '-1'은 목록의 마지막 값을 나타내고 '-2'는 마지막 값에서 두 번째 값을 나타냅니다. 예를 들어:

```python
>>> my_list[-1]
3
>>> my_list[-2]
2
>>> my_list[-3]
1
```

`append()` 함수를 사용하여 목록에 값을 추가할 수 있습니다.

```python
>>> my_list.append(4)
>>> my_list
[1, 2, 3, 4]
```

`remove()` 함수를 사용하여 목록에서 값을 제거할 수 있습니다.

```python
>>> my_list.remove(2)
>>> my_list
[1, 3, 4]
```

`sort()` 함수를 사용하여 목록을 정렬할 수도 있습니다.

```python
>>> my_list.sort()
>>> my_list
[1, 3, 4]
```

목록에서 사용할 수 있는 다른 많은 기능이 있습니다. [Python 설명서](https://docs.python.org/3/tutorial/datastructures.html)에서 전체 목록을 찾을 수 있습니다.

## 루프

루프는 코드 블록을 여러 번 실행할 수 있는 일종의 제어 흐름 문입니다. 파이썬에는 `for` 루프와 `while` 루프의 두 가지 유형의 루프가 있습니다.

'for' 루프는 일련의 값을 반복하는 데 사용됩니다. 예를 들어 `for` 루프를 사용하여 목록의 각 값을 인쇄할 수 있습니다.

```python
>>> my_list = [1, 2, 3, 4]
>>> for value in my_list:
...     print(value)
... 
1
2
3
4
```

위의 코드는 `1`, `2`, `3` 및 `4`를 별도의 줄에 인쇄합니다.

'while' 루프는 조건이 충족될 때까지 코드 블록을 실행하는 데 사용됩니다. 예를 들어 'while' 루프를 사용하여 특정 숫자에 도달할 때까지 숫자 목록을 인쇄할 수 있습니다.

```python
>>> num = 1
>>> while num <= 10:
...     print(num)
...     num = num + 1
... 
1
2
3
4
5
6
7
8
9
10
```

위의 코드는 '1'에서 '10'까지의 숫자를 별도의 줄에 인쇄합니다.

## 조건부

조건문은 특정 조건이 충족되는 경우에만 코드 블록을 실행할 수 있는 일종의 제어 흐름 문입니다. 파이썬에는 세 가지 유형의 조건문이 있습니다: `if` 문, `elif` 문 및 `else` 문.

'if' 문은 특정 조건이 'True'인 경우에만 코드 블록을 실행하는 데 사용됩니다. 예를 들어 'if' 문을 사용하여 특정 숫자가 양수인 경우에만 메시지를 출력할 수 있습니다.

```python
>>> num = 1
>>> if num > 0:
...     print("The number is positive.")
... 
The number is positive.
```

'elif' 문은 특정 조건이 'True'이고 이전 'if' 문이 'False'인 경우에만 코드 블록을 실행하는 데 사용됩니다. 예를 들어 숫자가 음수이면 'elif' 문을 사용하여 다른 메시지를 출력할 수 있습니다.

```python
>>> num = -1
>>> if num > 0:
...     print("The number is positive.")
... elif num < 0:
...     print("The number is negative.")
... 
The number is negative.
```

`else` 문은 이전 `if` 및 `elif` 문이 모두 `False`인 경우에만 코드 블록을 실행하는 데 사용됩니다. 예를 들어 숫자가 '0'인 경우 'else' 문을 사용하여 메시지를 출력할 수 있습니다.

```python
>>> num = 0
>>> if num > 0:
...     print("The number is positive.")
... elif num < 0:
...     print("The number is negative.")
... else:
...     print("The number is zero.")
... 
The number is zero.
```

## 기능

함수는 여러 번 실행할 수 있는 코드 블록입니다. Python에서는 `def` 키워드를 사용하여 자신만의 함수를 정의할 수 있습니다. 예를 들어 메시지를 인쇄하는 함수를 정의할 수 있습니다.

```python
>>> def print_message():
...     print("Hello, World!")
... 
>>> print_message()
Hello, World!
```

함수에 인수를 전달할 수도 있습니다. 인수는 함수가 호출될 때 함수에 전달되는 값입니다. 예를 들어 사용자 지정 문자열로 메시지를 인쇄하는 함수를 정의할 수 있습니다.

```python
>>> def print_message(message):
...     print(message)
... 
>>> print_message("Hello, World!")
Hello, World!
```

함수에서 값을 반환할 수도 있습니다. 반환 값은 함수를 호출한 코드로 다시 전달되는 값입니다. 예를 들어 두 숫자의 합을 계산하는 함수를 정의할 수 있습니다.

```python
>>> def add(num1, num2):
...     return num1 + num2
... 
>>> add(1, 2)
3
```

## 클래스

클래스는 개체를 만들기 위한 템플릿입니다. 객체는 자체 변수와 함수를 갖는 데이터 구조입니다. Python에서는 `class` 키워드를 사용하여 자신만의 클래스를 정의할 수 있습니다. 예를 들어 2차원 공간에서 점을 나타내는 클래스를 정의할 수 있습니다.

```python
>>> class Point:
...     def __init__(self, x, y):
...         self.x = x
...         self.y = y
... 
>>> point = Point(1, 2)
>>> print(point.x)
1
>>> print(point.y)
2
```

위의 코드에서 `Point`라는 클래스를 정의합니다. `__init__()` 함수는 개체를 초기화하는 데 사용되는 특수 함수입니다. `self` 키워드는 개체 자체를 참조하는 데 사용됩니다. `x` 및 `y` 변수는 객체의 속성이라고 합니다.

그런 다음 `point`라는 객체를 만들고 `x` 및 `y` 속성을 인쇄합니다.

클래스 내에서 함수를 정의할 수도 있습니다. 이러한 함수를 클래스의 메서드라고 합니다. 예를 들어 두 점 사이의 거리를 계산하는 방법을 정의할 수 있습니다.

```python
>>> class Point:
...     def __init__(self, x, y):
...         self.x = x
...         self.y = y
... 
...     def distance(self, other):
...         return ((self.x - other.x)**2 + (self.y - other.y)**2)**0.5
... 
>>> point1 = Point(1, 2)
>>> point2 = Point(4, 6)
>>> print(point1.distance(point2))
5.0
```

위의 코드에서 두 점 사이의 거리를 계산하는 `distance()`라는 메서드를 정의합니다. 그런 다음 두 개의 개체를 만들고 그 사이의 거리를 인쇄합니다.

## 자원

이 가이드는 Python 프로그래밍의 기본 사항만 다루었습니다. Python에 대해 자세히 알아보려면 다음 리소스를 확인하세요.

* [공식 Python 튜토리얼](https://docs.python.org/3/tutorial/)
* [공식 파이썬 문서](https://docs.python.org/3/)
* [Python 어려운 방법 배우기](https://learnpythonthehardway.org/python3/)
* [A Byte of Python](https://python.swaroopch.com/)
* [당신을 위한 파이썬](https://pythonyou.com/)