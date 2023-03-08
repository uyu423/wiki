---
title: wxPython
description: 
published: true
date: 2023-02-24T03:32:30.993Z
tags: 
editor: markdown
dateCreated: 2023-02-24T03:32:29.596Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [wxPython***English** document is available*](/en/Knowledge-base/Dictionary/wxpython)
{.links-list}



# 개요
wxPython은 Python 프로그래밍 언어용 GUI 툴킷입니다. 이를 통해 개발자는 Windows, Mac OS 및 Unix를 포함한 여러 플랫폼에서 기본 그래픽 사용자 인터페이스로 애플리케이션을 만들 수 있습니다. 무료로 사용하고 배포할 수 있는 오픈 소스 라이브러리입니다.

# 설명
wxPython은 널리 사용되는 wxWidgets 크로스 플랫폼 C++ 라이브러리의 래퍼입니다. 개발자가 기본 그래픽 사용자 인터페이스를 사용하여 응용 프로그램을 만들 수 있는 일련의 Python 클래스 및 기능을 제공합니다. Python 및 C++로 작성되었으며 Windows, Mac OS 및 Unix 플랫폼에서 사용할 수 있습니다.

wxPython 라이브러리는 다음과 같은 다양한 기능을 제공합니다.

- 버튼, 체크박스 및 텍스트 상자와 같은 GUI 컨트롤 세트
- 레이아웃 관리 및 창 위치 지정 지원
- 마우스 클릭과 같은 사용자 동작에 대한 이벤트 처리
- 맞춤형 그래픽 생성을 위한 그리기 기능
- 인쇄 및 드래그 앤 드롭 지원
- 클립보드 및 파일 시스템과 같은 기본 플랫폼 기능에 대한 액세스

wxPython은 또한 기본 wxWidgets 라이브러리 작업을 위한 여러 유틸리티 클래스 및 함수를 제공합니다. 여기에는 창, 대화 상자 및 프레임을 관리하는 기능과 클립보드 및 파일 시스템 작업을 위한 기능이 포함됩니다.

# 역사
wxPython은 원래 1998년 Robin Dunn에 의해 개발되었습니다. 처음에는 상용 제품으로 출시되었지만 이후 1999년에 오픈 소스 소프트웨어로 출시되었습니다.

# 특징
wxPython은 GUI 응용 프로그램을 만들기 위한 다양한 기능을 제공합니다. 여기에는 다음이 포함됩니다.

- 버튼, 체크박스 및 텍스트 상자와 같은 GUI 컨트롤 세트
- 레이아웃 관리 및 창 위치 지정 지원
- 마우스 클릭과 같은 사용자 동작에 대한 이벤트 처리
- 맞춤형 그래픽 생성을 위한 그리기 기능
- 인쇄 및 드래그 앤 드롭 지원
- 클립보드 및 파일 시스템과 같은 기본 플랫폼 기능에 대한 액세스
- 기본 wxWidgets 라이브러리 작업을 위한 유틸리티 클래스 및 함수

# 예
다음 예제는 wxPython을 사용하여 간단한 창을 만드는 방법을 보여줍니다.

```python
import wx

app = wx.App()

frame = wx.Frame(None, title="Hello World")
frame.Show()

app.MainLoop()
```

# 장점과 단점
wxPython의 주요 이점은 플랫폼 간 호환성입니다. 이를 통해 개발자는 Windows, Mac OS 및 Unix 플랫폼에서 실행되는 기본 그래픽 사용자 인터페이스로 애플리케이션을 만들 수 있습니다.

wxPython의 주요 단점은 Python 및 C++로 작성되어 디버그 및 유지 관리가 어려울 수 있다는 것입니다.

# 관련 기술
wxPython은 PyQt, Tkinter 및 wxWidgets와 같은 다른 GUI 툴킷과 관련이 있습니다. 또한 PyGTK 및 PyGame과 같은 다른 Python 라이브러리와 관련이 있습니다.