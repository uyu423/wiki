---
title: Python을 사용하여 그래픽 사용자 인터페이스(GUI) 개발
description: 
published: true
date: 2023-02-17T18:01:54.025Z
tags: 
editor: markdown
dateCreated: 2023-01-30T05:27:31.682Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Developing a Graphical User Interface (GUI) using Python***English** version of this document is available*](/en/Knowledge-base/Common/developing-a-graphical-user-interface-gui-using-python)
{.links-list}



## GUI란?

그래픽 사용자 인터페이스(GUI)는 사용자가 일반적으로 마우스와 같은 포인팅 장치를 사용하여 그래픽 방식으로 전자 장치와 상호 작용하여 전자 응용 프로그램을 제어할 수 있도록 하는 사용자 인터페이스 유형입니다.

GUI는 사용자가 명령을 배우고 입력해야 하는 명령줄 인터페이스(CLI)보다 사용자가 컴퓨터 응용 프로그램과 상호 작용할 수 있는 보다 직관적인 방법을 제공합니다. GUI는 또한 새로운 사용자가 응용 프로그램 사용을 쉽게 시작할 수 있도록 합니다.

Python에서 GUI를 만드는 것은 PyQt5라는 모듈을 사용하여 수행됩니다. PyQt5는 Qt v5용 포괄적인 Python 바인딩 세트입니다. Qt는 GUI 프로그램 개발에 널리 사용되는 크로스 플랫폼 애플리케이션 개발 프레임워크입니다.

## 파이썬에서 GUI를 만드는 방법

파이썬에서 GUI를 만드는 방법은 여러 가지가 있지만 가장 일반적으로 사용되는 모듈은 PyQt5입니다.

PyQt5는 Qt v5용 포괄적인 Python 바인딩 세트입니다. Qt는 GUI 프로그램 개발에 널리 사용되는 크로스 플랫폼 애플리케이션 개발 프레임워크입니다.

PyQt5를 사용하여 Python에서 기본 GUI를 만들려면 다음을 수행해야 합니다.

1. PyQt5 모듈을 가져옵니다.
2. QtWidgets.QApplication 인스턴스를 생성합니다.
3. QtWidgets.QWidget 인스턴스를 생성합니다.
4. 위젯의 속성을 설정합니다.
5. QtWidgets.QLabel 인스턴스를 추가하여 텍스트를 표시합니다.
6. QtWidgets.QPushButton 인스턴스를 추가하여 작업을 트리거합니다.
7. 버튼의 클릭 신호를 슬롯에 연결합니다.
8. 애플리케이션을 실행합니다.

각 단계를 자세히 살펴보겠습니다.

### PyQt5 모듈 가져오기

먼저 PyQt5 모듈을 가져와야 합니다. 다음 코드를 사용하여 이를 수행할 수 있습니다.

```
import PyQt5
```

### QtWidgets.QApplication 인스턴스 만들기

다음으로 QtWidgets.QApplication 인스턴스를 만들어야 합니다. 이 인스턴스는 애플리케이션의 제어 흐름 및 기본 설정 관리를 담당합니다.

QtWidgets.QApplication() 생성자를 호출하여 QApplication 인스턴스를 생성할 수 있습니다. sys.argv 매개변수를 사용하여 명령줄 인수를 전달해야 합니다.

```
import sys

app = QtWidgets.QApplication(sys.argv)
```

### QtWidgets.QWidget 인스턴스 만들기

QApplication 인스턴스가 있으면 QtWidgets.QWidget 인스턴스를 만들 수 있습니다. 이 위젯은 GUI의 기본 컨테이너가 됩니다.

QtWidgets.QWidget() 생성자를 호출하여 QWidget 인스턴스를 만들 수 있습니다.

```
widget = QtWidgets.QWidget()
```

### 위젯 속성 설정하기

QWidget 인스턴스가 있으면 해당 속성을 설정할 수 있습니다. 우리가 설정하는 가장 일반적인 속성은 위젯의 크기와 위치입니다.

QtWidgets.QWidget.resize() 메서드를 사용하여 위젯의 크기를 설정할 수 있습니다. 위젯의 너비와 높이를 픽셀 단위로 전달해야 합니다.

```
widget.resize(400, 300)
```

QtWidgets.QWidget.move() 메서드를 사용하여 위젯의 위치를 설정할 수 있습니다. 위젯의 x 및 y 좌표를 픽셀 단위로 전달해야 합니다.

```
widget.move(100, 100)
```

### QtWidgets.QLabel 인스턴스 추가

QWidget 인스턴스가 있으면 여기에 하위 위젯을 추가할 수 있습니다. QWidget에 추가하는 가장 일반적인 하위 위젯은 QtWidgets.QLabel입니다.

QLabel은 텍스트를 표시할 수 있는 위젯입니다. QtWidgets.QLabel() 생성자를 호출하여 QLabel을 만들 수 있습니다. 표시하려는 텍스트를 전달해야 합니다.

```
label = QtWidgets.QLabel("Hello, World!")
```

QLabel이 있으면 QtWidgets.QWidget.addWidget() 메서드를 사용하여 QWidget에 추가할 수 있습니다.

```
widget.addWidget(label)
```

### QtWidgets.QPushButton 인스턴스 추가

QWidget이 있으면 QtWidgets.QPushButton도 추가할 수 있습니다. QPushButton은 사용자가 클릭하여 작업을 트리거할 수 있는 위젯입니다.

QtWidgets.QPushButton() 생성자를 호출하여 QPushButton을 생성할 수 있습니다. 버튼에 표시할 텍스트를 전달해야 합니다.

```
button = QtWidgets.QPushButton("Click me!")
```

QPushButton이 있으면 QtWidgets.QWidget.addWidget() 메서드를 사용하여 QWidget에 추가할 수 있습니다.

```
widget.addWidget(button)
```

### 버튼의 클릭 신호를 슬롯에 연결

QPushButton이 있으면 클릭된 신호를 슬롯에 연결해야 합니다. 슬롯은 파이썬 콜러블입니다. 버튼을 클릭하면 슬롯이 호출됩니다.

QtCore.QObject.connect() 메서드를 사용하여 버튼의 클릭 신호를 슬롯에 연결할 수 있습니다. 버튼의 클릭 신호와 호출하려는 슬롯을 전달해야 합니다.

```
QtCore.QObject.connect(button, QtCore.SIGNAL("clicked()"), some_slot)
```

### 애플리케이션 실행

GUI를 만든 후에는 QtWidgets.QApplication.exec_() 메서드를 호출하여 실행할 수 있습니다.

```
app.exec_()
```

## 예

모든 단계를 함께 넣어 간단한 "Hello, World!"를 만들어 봅시다. GUI.

```
import sys
from PyQt5 import QtWidgets, QtCore

app = QtWidgets.QApplication(sys.argv)

widget = QtWidgets.QWidget()
widget.resize(400, 300)
widget.move(100, 100)

label = QtWidgets.QLabel("Hello, World!")
button = QtWidgets.QPushButton("Click me!")

widget.addWidget(label)
widget.addWidget(button)

QtCore.QObject.connect(button, QtCore.SIGNAL("clicked()"), some_slot)

widget.show()

app.exec_()
```

코드를 실행하면 다음과 같은 창이 표시됩니다.

![Hello, World!](https://github.com/mravendi/python_gui/raw/master/helloworld.png)

버튼을 클릭하면 some_slot() 함수가 호출됩니다.

## 결론

이 게시물에서는 PyQt5 모듈을 사용하여 Python에서 GUI를 만드는 기본 사항을 다뤘습니다. 우리는 QWidget을 생성하는 방법, 여기에 하위 위젯을 추가하는 방법 및 위젯의 신호를 슬롯에 연결하는 방법을 살펴보았습니다.