---
title: 가상 현실(VR) 경험을 만드는 방법
description: 
published: true
date: 2023-02-16T21:17:58.870Z
tags: 
editor: markdown
dateCreated: 2023-02-16T21:17:57.090Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [How to Create a Virtual Reality (VR) Experience***English** document is available*](/en/Knowledge-base/Common/how-to-create-a-virtual-reality-vr-experience)
{.links-list}


# 가상 현실(VR) 경험을 만드는 방법

최근 저렴하고 사용하기 쉬운 여러 VR 헤드셋이 출시되면서 VR 경험 개발을 시작하기에 지금보다 더 좋은 때는 없었습니다. 이 문서에서는 다양한 유형의 VR 헤드셋에 대한 개요와 처음부터 VR 경험을 만드는 방법을 포함하여 VR 개발을 시작하는 방법을 보여줍니다.

## VR 헤드셋의 종류

VR 헤드셋에는 테더링과 모바일의 두 가지 주요 유형이 있습니다. Oculus Rift 및 HTC Vive와 같은 테더링 헤드셋은 강력한 게임용 PC 또는 콘솔에 연결되며 VR 애플리케이션을 실행하려면 많은 처리 능력이 필요합니다. Samsung Gear VR 및 Google Daydream과 같은 모바일 헤드셋은 스마트폰을 디스플레이 및 처리 장치로 사용합니다. 모바일 VR은 더 저렴하고 시작하기 쉽지만 테더링 VR은 더 몰입감 있는 경험을 제공할 수 있습니다.

## VR 개발 시작하기

VR 개발을 막 시작했다면 모바일 VR 헤드셋으로 시작하는 것이 좋습니다. 이 헤드셋은 더 저렴하고 사용하기 쉬우며 사용할 수 있는 훌륭한 VR 응용 프로그램이 많이 있습니다.

VR 헤드셋이 있으면 VR SDK를 설치해야 합니다. 가장 인기 있는 VR SDK는 Oculus Mobile SDK, Google VR SDK 및 Unity 3D입니다. Oculus Mobile SDK는 Gear VR과 같은 Oculus 브랜드 헤드셋과만 호환됩니다. Google VR SDK는 Daydream, Cardboard 및 Gear VR을 비롯한 다양한 헤드셋과 호환됩니다. Unity 3D는 VR 개발을 지원하는 인기 있는 게임 엔진입니다.

VR 헤드셋과 SDK가 설치되면 VR 애플리케이션 개발을 시작할 준비가 된 것입니다. 시작하려면 다음 리소스 중 일부를 확인하는 것이 좋습니다.

- [Oculus 모바일 SDK 시작하기 가이드](https://developer.oculus.com/documentation/mobilesdk/latest/concepts/mobile-getting-started/)
- [Android용 Google VR SDK 시작 가이드](https://developers.google.com/vr/android/get-started)
- [Unity 3D VR 개발 가이드](https://learn.unity.com/tutorial/virtual-reality-development)

## 처음부터 VR 경험 만들기

이제 VR 헤드셋과 SDK가 설치되었으므로 VR 애플리케이션 개발을 시작할 준비가 되었습니다. 이 섹션에서는 기본 VR 경험을 처음부터 만드는 방법을 보여줍니다.

먼저 새 Unity 프로젝트를 만들어야 합니다. Unity를 열고 "새 프로젝트"를 클릭한 다음 프로젝트 이름을 지정합니다. 그런 다음 "가상 현실 지원" 확인란을 선택하고 "프로젝트 만들기"를 클릭합니다.

다음으로 장면을 만들어야 합니다. 장면은 VR 경험을 구성하는 개체의 모음입니다. 장면을 만들려면 Unity 메뉴에서 "GameObject" > "3D Object" > "Plane"을 선택합니다. 그러면 장면에 평면 개체가 생성됩니다.

이제 장면에 일부 콘텐츠를 추가해야 합니다. 이렇게 하려면 고유한 3D 모델을 만들거나 Unity 에셋 스토어에서 무료 에셋을 사용할 수 있습니다. 이 예에서는 Unity 에셋 스토어의 무료 에셋을 사용합니다. 씬에 에셋을 추가하려면 Unity 메뉴에서 "Assets" > "Import Package" > "Asset Store"를 선택합니다. 그러면 Unity 에셋 스토어 창이 열립니다. "무료 자산"을 검색하고 원하는 자산을 찾으십시오. 이 예에서는 "Free Low Poly Trees Pack" 자산을 사용합니다. 마음에 드는 자산을 찾으면 "가져오기"를 클릭하여 프로젝트에 추가하십시오.

자산을 가져오면 "Project" 창에서 "Hierarchy" 창으로 드래그하여 장면에 추가할 수 있습니다. 그러면 장면에 자산의 인스턴스가 생성됩니다.

일부 콘텐츠가 포함된 장면이 있으므로 상호 작용을 추가할 준비가 되었습니다. 이렇게 하려면 몇 가지 스크립트를 추가해야 합니다. 스크립트는 게임 개체에 수행할 작업을 알려주는 코드 조각입니다. 스크립트를 만들려면 Unity 메뉴에서 "자산" > "만들기" > "C# 스크립트"를 선택합니다. 스크립트 이름을 지정하고 "만들기"를 클릭합니다. 이렇게 하면 기본 코드 편집기에서 스크립트가 열립니다.

이 예에서는 플레이어가 나무를 볼 때 나무가 앞뒤로 흔들리는 스크립트를 추가합니다. 이를 위해 플레이어가 시선으로 게임을 제어할 수 있는 "Gaze" 입력 방법을 사용합니다.

먼저 스크립트에 Gaze 입력 방법을 인식하도록 코드를 추가해야 합니다. 스크립트에 다음 코드를 추가합니다.

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

다음으로 트리가 앞뒤로 흔들리도록 코드를 추가해야 합니다. 스크립트에 다음 코드를 추가합니다.

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

이 코드는 플레이어의 시선에 따라 나무가 앞뒤로 흔들리도록 합니다.

마지막으로 트리 개체에 스크립트를 추가해야 합니다. 이렇게 하려면 "계층 구조" 창에서 트리 개체를 선택하고 "구성 요소 추가" 버튼을 클릭합니다. 그런 다음 구성 요소 목록에서 "스크립트" > "TreeSwing"을 선택합니다.

이제 스크립트가 트리에 추가되었으므로 플레이어가 트리를 볼 때 트리가 앞뒤로 흔들립니다.

축하해요! 첫 번째 VR 경험을 만들었습니다.

## 더 읽을 수 있는 리소스

- [Oculus 모바일 SDK 시작하기 가이드](https://developer.oculus.com/documentation/mobilesdk/latest/concepts/mobile-getting-started/)
- [Android용 Google VR SDK 시작 가이드](https://developers.google.com/vr/android/get-started)
- [Unity 3D VR 개발 가이드](https://learn.unity.com/tutorial/virtual-reality-development)
- [Oculus Rift 개발자 가이드](https://developer.oculus.com/documentation/pcsdk/latest/concepts/index/)
- [HTC Vive 개발자 가이드](https://developer.vive.com/resources/knowledgebase/category_view/?catid=7)
- [삼성 Gear VR 개발자 가이드](https://developer.samsung.com/gear-vr)
- [Google Daydream 개발자 가이드](https://developers.google.com/daydream)