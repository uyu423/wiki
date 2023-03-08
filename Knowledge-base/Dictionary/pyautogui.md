---
title: PyAutoGUI
description: 
published: true
date: 2023-03-06T03:32:34.995Z
tags: 
editor: markdown
dateCreated: 2023-03-06T03:32:33.629Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [PyAutoGUI***English** document is available*](/en/Knowledge-base/Dictionary/pyautogui)
{.links-list}

# PyAutoGUI

## 개요
PyAutoGUI는 키보드 및 마우스 입력을 시뮬레이션하여 컴퓨터에서 작업 자동화를 가능하게 하는 Python 모듈입니다. 크로스 플랫폼 모듈이므로 Windows, macOS 및 Linux 운영 체제에서 사용할 수 있습니다.

## 설명
PyAutoGUI는 개발자가 키보드 및 마우스 입력을 시뮬레이션하여 컴퓨터에서 작업을 자동화할 수 있는 Python 모듈입니다. 양식 작성, 버튼 클릭, 텍스트 입력과 같은 반복적인 작업을 자동화하는 데 사용할 수 있습니다. PyAutoGUI는 소프트웨어 응용 프로그램을 테스트하는 데 사용할 수 있는 GUI 자동화 스크립트를 만드는 데에도 사용할 수 있습니다.

PyAutoGUI는 사용하기 쉽고 구문이 간단합니다. Python 패키지 관리자인 pip를 사용하여 설치할 수 있습니다. 일단 설치되면 개발자는 모듈을 가져와 Python 스크립트에서 사용할 수 있습니다.

PyAutoGUI는 키보드 및 마우스 입력을 시뮬레이션하기 위한 다양한 기능을 제공합니다. 이러한 기능에는 텍스트 입력, 키 누르기 및 놓기, 마우스 클릭 및 마우스 휠 스크롤이 포함됩니다. PyAutoGUI를 사용하여 화면에서 이미지를 찾고 마우스 클릭을 시뮬레이션할 수도 있습니다.

PyAutoGUI는 Python을 지원하는 모든 운영 체제에서 작업을 자동화하는 데 사용할 수 있습니다. 여기에는 Windows, macOS 및 Linux가 포함됩니다. PyAutoGUI는 가상 머신과 원격 서버에서 작업을 자동화하는 데에도 사용할 수 있습니다.

## 역사
PyAutoGUI는 2014년 Al Sweigart에 의해 만들어졌습니다. Al Sweigart는 소프트웨어 개발자이자 "Automate the Boring Stuff with Python"을 비롯한 여러 프로그래밍 서적의 저자입니다. PyAutoGUI는 그의 컴퓨터에서 작업을 자동화하기 위해 만들어졌으며 이후 컴퓨터에서 작업을 자동화하기 위한 인기 있는 모듈이 되었습니다.

## 특징
- 키보드 및 마우스 입력 시뮬레이션
- 크로스 플랫폼 모듈
- 사용하기 쉽고 간단한 구문
- 키보드 및 마우스 입력 시뮬레이션을 위한 다양한 기능 제공
- 화면에서 이미지를 찾고 마우스 클릭을 시뮬레이션할 수 있습니다.
- 가상 머신 및 원격 서버에서 작업을 자동화하는 데 사용할 수 있습니다.

## 예
다음 예제는 PyAutoGUI를 사용하여 컴퓨터에서 작업을 자동화하는 방법을 보여줍니다.

```python
import pyautogui

# Click on the Start menu
pyautogui.click(50, 100)

# Type "notepad" and press Enter
pyautogui.typewrite("notepad")
pyautogui.press("enter")

# Type some text in Notepad
pyautogui.typewrite("Hello, World!")

# Save the file
pyautogui.hotkey("ctrl", "s")
pyautogui.typewrite("example.txt")
pyautogui.press("enter")
```

이 예제는 시작 메뉴를 클릭하고 메모장을 열고 일부 텍스트를 입력하고 파일을 저장합니다.

## 장점과 단점
### 장점
- 사용하기 쉽고 간단한 구문
- 크로스 플랫폼 모듈
- 키보드 및 마우스 입력 시뮬레이션을 위한 다양한 기능 제공
- 화면에서 이미지를 찾고 마우스 클릭을 시뮬레이션할 수 있습니다.
- 가상 머신 및 원격 서버에서 작업을 자동화하는 데 사용할 수 있습니다.

### 단점
- 복잡한 자동화 작업에는 적합하지 않을 수 있음
- 보안 기능이 있는 일부 애플리케이션에서는 작동하지 않을 수 있습니다.

## 관련 기술
PyAutoGUI는 종종 컴퓨터에서 작업을 자동화하기 위해 다른 Python 모듈과 함께 사용됩니다. 일부 관련 기술은 다음과 같습니다.
- Selenium: 웹 브라우저 자동화를 위한 Python 모듈입니다.
- Pywinauto: Windows GUI 응용 프로그램을 자동화하기 위한 Python 모듈입니다.
- PyAutoIt: AutoIt을 사용하여 Windows GUI 응용 프로그램을 자동화하기 위한 Python 모듈입니다.

## 여담
PyAutoGUI는 컴퓨터에서 작업을 자동화하는 강력한 도구입니다. 그러나 책임감 있고 윤리적으로 사용하는 것이 중요합니다. 불법적이거나 비윤리적인 작업을 자동화하면 심각한 결과를 초래할 수 있습니다. 또한 개발자는 자동화와 관련된 보안 위험을 인식하고 시스템을 보호하기 위한 조치를 취해야 합니다.

## 기타
PyAutoGUI는 컴퓨터에서 작업을 자동화하는 데 널리 사용되는 모듈입니다. 사용하기 쉽고 구문이 단순하여 초보자에게 훌륭한 도구입니다. 그러나 복잡한 자동화 작업에는 적합하지 않을 수 있으며 보안 기능이 있는 일부 응용 프로그램에서는 작동하지 않을 수 있습니다. 또한 개발자는 자동화와 관련된 보안 위험을 인식하고 시스템을 보호하기 위한 조치를 취해야 합니다.