---
title: 使用 Xamarin 开发跨平台移动应用程序
description: 
published: true
date: 2023-01-31T11:57:41.129Z
tags: 
editor: markdown
dateCreated: 2023-01-31T11:57:39.512Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}

- [Developing Cross-Platform Mobile Apps with Xamarin***English** version of this document is available*](/en/Knowledge-base/Common/developing-cross-platform-mobile-apps-with-xamarin)
{.links-list}



# 使用 Xamarin 开发跨平台移动应用程序

Xamarin 是一种跨平台开发工具，允许开发人员使用 C# 创建适用于 Android 和 iOS 的本机应用程序。在本文中，我们将讨论使用 Xamarin 进行跨平台移动开发的好处，并提供实用的入门指南。

## 为什么使用 Xamarin？

考虑将 Xamarin 用于下一个移动开发项目的原因有多种：

- **Xamarin 是免费和开源的** - Xamarin 可以免费使用，即使是商业项目也是如此。此外，Xamarin 平台是开源的，这意味着您可以根据需要为其开发做出贡献。

- **Xamarin 具有出色的语言支持** - Xamarin 使用 C# 编程语言，这是一种设计良好、功能强大且现代的语言。 C# 对面向对象的编程提供了出色的支持，还具有 LINQ 等函数式编程功能。

- **Xamarin 拥有出色的工具** - Xamarin 开发环境包含开发、测试和部署应用程序所需的一切。 Xamarin Studio IDE 与 Visual Studio 类似，提供出色的开发体验。

- **Xamarin 拥有强大的社区支持** - 有一个庞大而活跃的 Xamarin 社区可以提供支持和帮助。

## Xamarin 入门

在本节中，我们将介绍设置 Xamarin 开发环境和创建简单的“Hello, World”应用程序的过程。

###先决条件

在我们开始之前，您需要做一些事情：

- 运行 Windows 或 macOS 的计算机
- 一个有效的 Microsoft 帐户（登录 Visual Studio 需要）

### 安装 Xamarin 平台

我们需要做的第一件事是安装 Xamarin 平台。最简单的方法是下载并安装 Microsoft 的 Visual Studio IDE。

安装 Visual Studio 后，启动它并使用您的 Microsoft 帐户登录。登录后，您将看到 Visual Studio 欢迎屏幕。单击“安装”按钮开始安装过程。

![Visual Studio 欢迎屏幕](https://i.imgur.com/p0sU6Tv.png)

安装过程完成后，系统会提示您重新启动计算机。计算机重新启动后，再次启动 Visual Studio 并单击“创建新项目”按钮。

![在 Visual Studio 中创建一个新项目](https://i.imgur.com/7bTzC4I.png)

在“新建项目”对话框中，选择“跨平台”选项卡，然后选择“空白应用程序（Android、iOS、Windows）”模板。为您的项目命名，然后单击“创建”按钮。

![在 Visual Studio 中创建一个新的 Xamarin 项目](https://i.imgur.com/eLFgU6O.png)

此时，您将看到一个对话框，询问您要面向哪个平台。对于此示例，我们将只选择 Android 和 iOS。如果您也想以该平台为目标，也可以选择 Windows。

![为我们的 Xamarin 项目选择目标平台](https://i.imgur.com/KzZ7bVx.png)

选择目标平台后，单击“创建”按钮，Visual Studio 将创建新项目。

### 编写代码

现在我们已经设置了项目，我们可以开始编写一些代码了。在“解决方案资源管理器”窗口中，展开“MainPage.xaml”文件并双击“MainPage.xaml.cs”文件以在编辑器中将其打开。

用以下代码替换“MainPage.xaml.cs”文件的内容：

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

此代码定义了一个简单的“Hello, World”标签，该标签将显示在屏幕中央。

### 测试应用程序

现在我们已经编写了一些代码，让我们测试我们的应用程序以确保它按预期工作。在 Visual Studio 中，选择“Debug”菜单，然后选择“Start Without Debugging”菜单项。

![无需在 Visual Studio 中调试即可启动 Xamarin 应用程序](https://i.imgur.com/W2nJNcu.png)

Visual Studio 现在将在选定的模拟器或仿真器中启动应用程序。你应该看到“你好，世界！”屏幕中央的标签。

![“你好，世界！”在 iOS 模拟器中运行的应用](https://i.imgur.com/5MWK0bY.png)

恭喜！你刚刚使用 Xamarin 创建了你的第一个跨平台移动应用程序。

## 结论

在本文中，我们讨论了使用 Xamarin 进行跨平台移动开发的好处，并提供了实用的入门指南。 Xamarin 是使用单个代码库为多个平台创建本机应用程序的绝佳工具。