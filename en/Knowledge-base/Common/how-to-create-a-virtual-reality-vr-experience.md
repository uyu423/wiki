---
title: How to Create a Virtual Reality (VR) Experience
description: 
published: true
date: 2023-02-16T21:18:05.366Z
tags: 
editor: markdown
dateCreated: 2023-02-16T21:17:57.111Z
---

- [Cómo crear una experiencia de realidad virtual (VR)***Spanish** document is available*](/es/Knowledge-base/Common/how-to-create-a-virtual-reality-vr-experience)
{.links-list}
- [如何创建虚拟现实 (VR) 体验***Chinese Simplified** document is available*](/zh/Knowledge-base/Common/how-to-create-a-virtual-reality-vr-experience)
{.links-list}
- [가상 현실(VR) 경험을 만드는 방법***Korean** document is available*](/ko/Knowledge-base/Common/how-to-create-a-virtual-reality-vr-experience)
{.links-list}


# How to Create a Virtual Reality (VR) Experience

With the recent release of several affordable and approachable VR headsets, there's never been a better time to get started with developing VR experiences. In this article, we'll show you how to get started with developing for VR, including an overview of the different types of VR headsets and how to create a VR experience from scratch.

## Types of VR Headsets

There are two main types of VR headsets: tethered and mobile. Tethered headsets, like the Oculus Rift and HTC Vive, are connected to a powerful gaming PC or console and require a lot of processing power to run VR applications. Mobile headsets, like the Samsung Gear VR and Google Daydream, use a smartphone as the display and processing unit. Mobile VR is more affordable and easier to get started with, but tethered VR can offer a more immersive experience.

## Getting Started with VR Development

If you're just getting started with VR development, we recommend starting with a mobile VR headset. These headsets are more affordable and easier to use, and there are plenty of great VR applications available for them.

Once you have a VR headset, you'll need to install a VR SDK. The most popular VR SDKs are Oculus Mobile SDK, Google VR SDK, and Unity 3D. Oculus Mobile SDK is only compatible with Oculus-branded headsets, like the Gear VR. Google VR SDK is compatible with a wide range of headsets, including the Daydream, Cardboard, and Gear VR. Unity 3D is a popular game engine that has built-in support for VR development.

Once you have a VR headset and SDK installed, you're ready to start developing VR applications. We recommend checking out some of the following resources to get started:

- The [Oculus Mobile SDK Getting Started Guide](https://developer.oculus.com/documentation/mobilesdk/latest/concepts/mobile-getting-started/)
- The [Google VR SDK for Android Getting Started Guide](https://developers.google.com/vr/android/get-started)
- The [Unity 3D VR Development Guide](https://learn.unity.com/tutorial/virtual-reality-development)

## Creating a VR Experience from Scratch

Now that you have a VR headset and SDK installed, you're ready to start developing VR applications. In this section, we'll show you how to create a basic VR experience from scratch.

First, you'll need to create a new Unity project. Open Unity, click "New Project," and name your project. Then, select the "Virtual Reality Supported" checkbox and click "Create Project."

Next, you'll need to create a scene. A scene is a collection of objects that make up your VR experience. To create a scene, select "GameObject" > "3D Object" > "Plane" from the Unity menu. This will create a plane object in your scene.

Now, you'll need to add some content to your scene. To do this, you can either create your own 3D models or use free assets from the Unity Asset Store. For this example, we'll use a free asset from the Unity Asset Store. To add an asset to your scene, select "Assets" > "Import Package" > "Asset Store" from the Unity menu. This will open the Unity Asset Store window. Search for "free assets" and find an asset that you like. For this example, we'll use the "Free Low Poly Trees Pack" asset. Once you've found an asset that you like, click "Import" to add it to your project.

Once the asset is imported, you can add it to your scene by dragging it from the "Project" window into the "Hierarchy" window. This will create an instance of the asset in your scene.

Now that you have a scene with some content, you're ready to add some interactivity. To do this, you'll need to add some scripts. A script is a piece of code that tells your game objects what to do. To create a script, select "Assets" > "Create" > "C# Script" from the Unity menu. Name your script and click "Create." This will open the script in your default code editor.

For this example, we'll add a script that makes our tree swing back and forth when the player looks at it. To do this, we'll use the "Gaze" input method, which lets the player control the game with their gaze.

First, we'll need to add some code to our script to make it aware of the Gaze input method. Add the following code to your script:

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

Next, we'll need to add some code to make our tree swing back and forth. Add the following code to your script:

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

This code will make our tree swing back and forth based on the player's gaze.

Finally, we'll need to add our script to our tree object. To do this, select the tree object in the "Hierarchy" window and click the "Add Component" button. Then, select "Scripts" > "TreeSwing" from the list of components.

Now that our script is added to our tree, our tree will swing back and forth when the player looks at it.

Congratulations! You've just created your first VR experience.

## Resources for Further Reading

- The [Oculus Mobile SDK Getting Started Guide](https://developer.oculus.com/documentation/mobilesdk/latest/concepts/mobile-getting-started/)
- The [Google VR SDK for Android Getting Started Guide](https://developers.google.com/vr/android/get-started)
- The [Unity 3D VR Development Guide](https://learn.unity.com/tutorial/virtual-reality-development)
- The [Oculus Rift Developer Guide](https://developer.oculus.com/documentation/pcsdk/latest/concepts/index/)
- The [HTC Vive Developer Guide](https://developer.vive.com/resources/knowledgebase/category_view/?catid=7)
- The [Samsung Gear VR Developer Guide](https://developer.samsung.com/gear-vr)
- The [Google Daydream Developer Guide](https://developers.google.com/daydream)