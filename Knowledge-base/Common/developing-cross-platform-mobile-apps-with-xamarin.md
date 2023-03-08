---
title: Xamarin을 사용하여 플랫폼 간 모바일 앱 개발
description: 
published: true
date: 2023-01-31T11:57:41.127Z
tags: 
editor: markdown
dateCreated: 2023-01-31T11:57:39.510Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Developing Cross-Platform Mobile Apps with Xamarin***English** version of this document is available*](/en/Knowledge-base/Common/developing-cross-platform-mobile-apps-with-xamarin)
{.links-list}



# Xamarin으로 크로스 플랫폼 모바일 앱 개발

Xamarin은 개발자가 C#을 사용하여 Android 및 iOS용 네이티브 애플리케이션을 만들 수 있는 플랫폼 간 개발 도구입니다. 이 문서에서는 플랫폼 간 모바일 개발에 Xamarin을 사용하는 이점에 대해 설명하고 시작하기 위한 실용적인 가이드를 제공합니다.

## Xamarin을 사용하는 이유

다음 모바일 개발 프로젝트에 Xamarin 사용을 고려해야 하는 몇 가지 이유가 있습니다.

- **Xamarin은 무료이며 오픈 소스입니다** - Xamarin은 상용 프로젝트에서도 무료로 사용할 수 있습니다. 또한 Xamarin 플랫폼은 오픈 소스이므로 원하는 경우 개발에 기여할 수 있습니다.

- **Xamarin은 우수한 언어 지원을 제공합니다** - Xamarin은 잘 설계되고 강력하며 현대적인 언어인 C# 프로그래밍 언어를 사용합니다. C#은 개체 지향 프로그래밍을 훌륭하게 지원하며 LINQ와 같은 함수형 프로그래밍 기능도 제공합니다.

- **Xamarin에는 훌륭한 도구가 있습니다** - Xamarin 개발 환경에는 애플리케이션을 개발, 테스트 및 배포하는 데 필요한 모든 것이 포함되어 있습니다. Xamarin Studio IDE는 Visual Studio와 유사하며 뛰어난 개발 환경을 제공합니다.

- **Xamarin은 강력한 커뮤니티 지원을 제공합니다** - 지원 및 지원을 제공할 수 있는 크고 활동적인 Xamarin 커뮤니티가 있습니다.

## Xamarin 시작하기

이 섹션에서는 Xamarin 개발 환경을 설정하고 간단한 "Hello, World" 애플리케이션을 만드는 과정을 살펴보겠습니다.

### 전제 조건

시작하기 전에 필요한 몇 가지 사항이 있습니다.

- Windows 또는 macOS를 실행하는 컴퓨터
- 유효한 Microsoft 계정(Visual Studio에 로그인하는 데 필요)

### Xamarin 플랫폼 설치

가장 먼저 해야 할 일은 Xamarin 플랫폼을 설치하는 것입니다. 가장 쉬운 방법은 Microsoft의 Visual Studio IDE를 다운로드하여 설치하는 것입니다.

Visual Studio가 설치되면 시작하고 Microsoft 계정으로 로그인합니다. 로그인하면 Visual Studio 시작 화면이 표시됩니다. 설치 프로세스를 시작하려면 "설치" 버튼을 클릭하십시오.

![Visual Studio 시작 화면](https://i.imgur.com/p0sU6Tv.png)

설치 프로세스가 완료되면 컴퓨터를 다시 시작하라는 메시지가 표시됩니다. 컴퓨터가 다시 시작되면 Visual Studio를 다시 시작하고 "새 프로젝트 만들기" 버튼을 클릭합니다.

![Visual Studio에서 새 프로젝트 만들기](https://i.imgur.com/7bTzC4I.png)

"New Project" 대화 상자에서 "Cross-Platform" 탭을 선택한 다음 "Blank App (Android, iOS, Windows)" 템플릿을 선택합니다. 프로젝트 이름을 지정하고 "만들기" 버튼을 클릭합니다.

![Visual Studio에서 새 Xamarin 프로젝트 만들기](https://i.imgur.com/eLFgU6O.png)

이 시점에서 대상 플랫폼을 묻는 대화 상자가 표시됩니다. 이 예에서는 Android와 iOS만 선택하겠습니다. 해당 플랫폼도 대상으로 지정하려는 경우 Windows를 선택할 수도 있습니다.

![Xamarin 프로젝트의 대상 플랫폼 선택](https://i.imgur.com/KzZ7bVx.png)

대상 플랫폼을 선택한 후 "만들기" 버튼을 클릭하면 Visual Studio에서 새 프로젝트를 만듭니다.

### 코드 작성

이제 프로젝트가 설정되었으므로 일부 코드 작성을 시작할 수 있습니다. "솔루션 탐색기" 창에서 "MainPage.xaml" 파일을 확장하고 "MainPage.xaml.cs" 파일을 두 번 클릭하여 편집기에서 엽니다.

"MainPage.xaml.cs" 파일의 내용을 다음 코드로 바꿉니다.

```csharp
using System;

using Xamarin.Forms;

namespace HelloWorld
{
    public class MainPage : ContentPage
    {
        public MainPage()
        {
            Content = new Label
            {
                Text = "Hello, World!",
                HorizontalOptions = LayoutOptions.Center,
                VerticalOptions = LayoutOptions.Center
            };
        }
    }
}
```

이 코드는 화면 중앙에 표시될 간단한 "Hello, World" 레이블을 정의합니다.

### 앱 테스트

이제 몇 가지 코드를 작성했으므로 앱이 예상대로 작동하는지 테스트해 보겠습니다. Visual Studio에서 "디버그" 메뉴를 선택한 다음 "디버깅하지 않고 시작" 메뉴 항목을 선택합니다.

![Visual Studio에서 디버깅하지 않고 Xamarin 앱 시작](https://i.imgur.com/W2nJNcu.png)

이제 Visual Studio가 선택한 시뮬레이터 또는 에뮬레이터에서 앱을 시작합니다. "Hello, World!" 메시지가 표시되어야 합니다. 화면 중앙의 라벨.

!["Hello, World!" iOS 시뮬레이터에서 실행 중인 앱](https://i.imgur.com/5MWK0bY.png)

축하합니다! Xamarin을 사용하여 첫 번째 플랫폼 간 모바일 앱을 만들었습니다.

## 결론

이 문서에서는 플랫폼 간 모바일 개발에 Xamarin을 사용하는 이점에 대해 논의하고 시작하기 위한 실용적인 가이드를 제공했습니다. Xamarin은 단일 코드베이스를 사용하여 여러 플랫폼을 위한 네이티브 애플리케이션을 만들기 위한 훌륭한 도구입니다.