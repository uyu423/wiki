---
title: PyInstaller
description: 
published: true
date: 2023-02-07T04:19:01.694Z
tags: 
editor: markdown
dateCreated: 2023-02-07T04:18:59.643Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [PyInstaller***English** document is available*](/en/Knowledge-base/Dictionary/pyinstaller)
{.links-list}


# 개요
PyInstaller는 Windows, Mac 및 Linux에서 Python 프로그램을 독립형 실행 파일로 패키징하는 프로그램입니다. Python이 설치되어 있거나 설치되어 있지 않은 사용자에게 응용 프로그램을 배포해야 하는 Python 개발자가 사용하도록 설계되었습니다.

# 설명
PyInstaller는 Python 프로그램을 독립형 실행 파일로 변환하기 위한 무료 오픈 소스 도구입니다. Python이 설치되어 있거나 설치되어 있지 않은 사용자에게 응용 프로그램을 배포해야 하는 Python 개발자가 사용하도록 설계되었습니다. 이 프로그램은 Python 프로그램을 분석하고 이를 실행하는 데 필요한 필수 파일과 라이브러리를 수집하여 작동합니다. 그런 다음 이러한 파일을 Python 설치 여부에 관계없이 모든 컴퓨터에서 실행할 수 있는 단일 실행 파일로 패키징합니다.

PyInstaller는 Python 2.7, 3.4, 3.5, 3.6 및 3.7을 지원하며 Windows, Mac 및 Linux용 애플리케이션을 패키징할 수 있습니다. 또한 Python 프로그램을 단일 파일 실행 파일로 패키징할 수 있으므로 소스 코드를 공개하지 않고 응용 프로그램을 배포하는 데 유용할 수 있습니다.

# 역사
PyInstaller는 2005년에 처음 출시되었으며 현재 자원 봉사 팀에 의해 유지 관리되고 있습니다. 2020년 기준으로 200만 회 이상의 다운로드를 기록하며 초기 출시 이후 꾸준히 인기를 얻고 있습니다.

# 특징
PyInstaller에는 Python 개발자에게 유용한 여러 기능이 있습니다. 여기에는 다음이 포함됩니다.

- 다중 플랫폼 지원: PyInstaller는 Windows, Mac 및 Linux용 애플리케이션을 패키징할 수 있습니다.
- 단일 파일 실행 파일: PyInstaller는 Python 프로그램을 단일 파일 실행 파일로 패키징할 수 있으며, 이는 소스 코드를 공개하지 않고 응용 프로그램을 배포하는 데 유용할 수 있습니다.
- 자동 종속성 감지: PyInstaller는 Python 프로그램을 실행하는 데 필요한 필수 파일과 라이브러리를 자동으로 감지하고 패키징합니다.
- 번들 Python 인터프리터: PyInstaller는 Python 인터프리터를 응용 프로그램과 함께 번들로 제공하여 Python이 설치되지 않은 컴퓨터에서 실행할 수 있습니다.

# 예
이 예제에서는 PyInstaller를 사용하여 간단한 Python 프로그램을 독립 실행형 실행 파일로 패키징합니다. 프로그램은 "Hello, world!"라는 문자열을 인쇄합니다. 콘솔에.

먼저 다음 내용으로 "hello.py"라는 파일을 만듭니다.

```
print("Hello, world!")
```

다음으로 다음 명령을 실행하여 프로그램을 독립 실행형 실행 파일로 패키징합니다.

```
pyinstaller hello.py
```

PyInstaller는 실행 파일을 포함하는 "dist"라는 폴더를 생성합니다. 이 파일은 Python 설치 여부에 관계없이 모든 컴퓨터에서 실행할 수 있습니다.

# 장점과 단점
장점

- 사용하기 쉬움: PyInstaller는 사용하기 쉽고 최소한의 설정만 필요합니다.
- 크로스 플랫폼: PyInstaller는 Windows, Mac 및 Linux용 애플리케이션을 패키징할 수 있습니다.
- 단일 파일 실행 파일: PyInstaller는 Python 프로그램을 단일 파일 실행 파일로 패키징할 수 있으며, 이는 소스 코드를 공개하지 않고 응용 프로그램을 배포하는 데 유용할 수 있습니다.

단점

- 제한된 지원: PyInstaller는 Python 2.7, 3.4, 3.5, 3.6 및 3.7만 지원합니다.
- GUI 없음: PyInstaller에는 GUI가 없으므로 명령줄에서 사용해야 합니다.

# 관련 기술
PyOxidizer는 Python 프로그램을 독립형 실행 파일로 패키징하는 또 다른 도구입니다. PyInstaller보다 강력하고 기능이 풍부하도록 설계되었지만 아직 초기 개발 단계입니다.