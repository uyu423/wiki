---
title: 如何创建虚拟现实 (VR) 体验
description: 
published: true
date: 2023-02-16T21:17:59.388Z
tags: 
editor: markdown
dateCreated: 2023-02-16T21:17:57.110Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [How to Create a Virtual Reality (VR) Experience***English** document is available*](/en/Knowledge-base/Common/how-to-create-a-virtual-reality-vr-experience)
{.links-list}


# 如何创建虚拟现实 (VR) 体验

随着最近发布的几款经济实惠且易于使用的 VR 耳机，现在是开始开发 VR 体验的最佳时机。在本文中，我们将向您展示如何开始进行 VR 开发，包括对不同类型 VR 耳机的概述以及如何从头开始创建 VR 体验。

## VR 耳机的类型

有两种主要类型的 VR 耳机：系留和移动。系留耳机，如 Oculus Rift 和 HTC Vive，连接到功能强大的游戏 PC 或控制台，需要大量处理能力才能运行 VR 应用程序。三星 Gear VR 和谷歌 Daydream 等移动耳机使用智能手机作为显示和处理单元。移动 VR 更实惠且更容易上手，但有线 VR 可以提供更身临其境的体验。

## VR 开发入门

如果您刚刚开始 VR 开发，我们建议您从移动 VR 耳机开始。这些耳机价格更实惠且更易于使用，并且有许多出色的 VR 应用程序可供使用。

拥有 VR 耳机后，您需要安装 VR SDK。最流行的 VR SDK 是 Oculus Mobile SDK、Google VR SDK 和 Unity 3D。 Oculus Mobile SDK 仅与 Oculus 品牌的耳机兼容，例如 Gear VR。 Google VR SDK 兼容多种头显，包括 Daydream、Cardboard 和 Gear VR。 Unity 3D 是一种流行的游戏引擎，内置了对 VR 开发的支持。

安装 VR 耳机和 SDK 后，您就可以开始开发 VR 应用程序了。我们建议您查看以下一些资源以开始使用：

- [Oculus Mobile SDK 入门指南](https://developer.oculus.com/documentation/mobilesdk/latest/concepts/mobile-getting-started/)
- [Google VR SDK for Android 入门指南](https://developers.google.com/vr/android/get-started)
- [Unity 3D VR开发指南](https://learn.unity.com/tutorial/virtual-reality-development)

## 从头开始创建 VR 体验

现在您已经安装了 VR 耳机和 SDK，您可以开始开发 VR 应用程序了。在本节中，我们将向您展示如何从头开始创建基本的 VR 体验。

首先，您需要创建一个新的 Unity 项目。打开 Unity，单击“新建项目”，然后为您的项目命名。然后，选中“支持虚拟现实”复选框并单击“创建项目”。

接下来，您需要创建一个场景。场景是构成 VR 体验的对象集合。要创建场景，请从 Unity 菜单中选择“GameObject”>“3D Object”>“Plane”。这将在您的场景中创建一个平面对象。

现在，您需要向场景中添加一些内容。为此，您可以创建自己的 3D 模型或使用 Unity Asset Store 中的免费资源。对于此示例，我们将使用来自 Unity Asset Store 的免费资产。要将资产添加到您的场景，请从 Unity 菜单中选择“资产”>“导入包”>“资产商店”。这将打开 Unity Asset Store 窗口。搜索“免费资产”并找到您喜欢的资产。对于此示例，我们将使用“Free Low Poly Trees Pack”资源。找到您喜欢的资产后，单击“导入”将其添加到您的项目中。

导入资产后，您可以通过将其从“项目”窗口拖到“层次结构”窗口中来将其添加到场景中。这将在您的场景中创建资产实例。

现在您已经有了包含一些内容的场景，您可以添加一些交互性了。为此，您需要添加一些脚本。脚本是一段代码，告诉您的游戏对象要做什么。要创建脚本，请从 Unity 菜单中选择“资产”>“创建”>“C# 脚本”。为您的脚本命名并单击“创建”。这将在您的默认代码编辑器中打开脚本。

对于此示例，我们将添加一个脚本，使我们的树在玩家注视时来回摆动。为此，我们将使用“注视”输入法，让玩家可以通过注视来控制游戏。

首先，我们需要向脚本中添加一些代码以使其识别注视输入法。将以下代码添加到您的脚本中：

```csharp
public class TreeSwing : MonoBehaviour {

// Use this for initialization
void Start () {
	
}

// Update is called once per frame
void Update () {
	
}
}
```

接下来，我们需要添加一些代码来让我们的树来回摆动。将以下代码添加到您的脚本中：

```csharp
public class TreeSwing : MonoBehaviour {

public float swingAmount = 10.0f;

// Use this for initialization
void Start () {
	
}

// Update is called once per frame
void Update () {
	transform.rotation = 
		Quaternion.Euler(0, Input.GetAxis("Horizontal") * swingAmount, 0);
}
}
```

这段代码将使我们的树根据玩家的视线来回摆动。

最后，我们需要将我们的脚本添加到我们的树对象中。为此，在“层次结构”窗口中选择树对象并单击“添加组件”按钮。然后，从组件列表中选择“脚本”>“TreeSwing”。

现在我们的脚本已添加到我们的树中，当玩家注视它时，我们的树会来回摆动。

恭喜！您刚刚创建了第一个 VR 体验。

## 进一步阅读的资源

- [Oculus Mobile SDK 入门指南](https://developer.oculus.com/documentation/mobilesdk/latest/concepts/mobile-getting-started/)
- [Google VR SDK for Android 入门指南](https://developers.google.com/vr/android/get-started)
- [Unity 3D VR开发指南](https://learn.unity.com/tutorial/virtual-reality-development)
- [Oculus Rift 开发者指南](https://developer.oculus.com/documentation/pcsdk/latest/concepts/index/)
- [HTC Vive 开发者指南](https://developer.vive.com/resources/knowledgebase/category_view/?catid=7)
- [三星 Gear VR 开发者指南](https://developer.samsung.com/gear-vr)
- [Google Daydream 开发者指南](https://developers.google.com/daydream)