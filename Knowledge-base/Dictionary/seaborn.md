---
title: Seaborn
description: 
published: true
date: 2023-02-07T03:56:58.816Z
tags: 
editor: markdown
dateCreated: 2023-02-07T03:56:52.459Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Seaborn***English** document is available*](/en/Knowledge-base/Dictionary/seaborn)
{.links-list}


# 개요
Seaborn은 matplotlib 기반의 Python 데이터 시각화 라이브러리입니다. 매력적이고 유익한 통계 그래픽을 그리기 위한 높은 수준의 인터페이스를 제공합니다.

# 설명
Seaborn은 matplotlib 기반의 Python 데이터 시각화 라이브러리입니다. 매력적이고 유익한 통계 그래픽을 그리기 위한 높은 수준의 인터페이스를 제공합니다. Seaborn은 matplotlib 위에 구축되었으며 pandas 데이터 구조와 밀접하게 통합되었습니다.

Seaborn은 최소한의 노력으로 매력적인 비주얼리제이션을 신속하게 생성할 수 있는 다양한 맞춤형 테마와 높은 수준의 인터페이스를 제공합니다. 또한 바이올린 플롯, 상자 플롯 및 쌍 플롯과 같은 몇 가지 특수한 플롯 유형을 제공합니다.

Seaborn은 또한 자동 색상 팔레트, 통계 추정 및 선형 관계 시각화와 같은 몇 가지 고급 기능을 제공합니다. 또한 라이브러리를 사용하면 요소의 크기, 모양 및 색상을 변경하는 옵션을 사용하여 플롯의 모양을 쉽게 사용자 정의할 수 있습니다.

# 역사
Seaborn은 2014년 Stanford University의 신경과학 박사후 연구원인 Michael Waskom이 만들었습니다. 이 라이브러리는 강력하지만 낮은 수준의 matplotlib 라이브러리와 사용하기 쉽지만 제한적인 pandas의 시각화 기능 사이의 격차를 메우기 위해 만들어졌습니다.

# 특징
Seaborn은 매력적이고 유익한 통계 그래픽을 만들기 위한 다양한 기능을 제공합니다. 라이브러리는 바이올린 플롯, 상자 플롯 및 쌍 플롯과 같은 여러 특수 플롯 유형을 지원합니다. 또한 자동 색상 팔레트, 통계 추정 및 선형 관계 시각화와 같은 몇 가지 고급 기능을 제공합니다.

Seaborn은 또한 사용자 지정 가능한 다양한 테마를 제공하므로 최소한의 노력으로 매력적인 시각화를 쉽고 빠르게 만들 수 있습니다. 또한 라이브러리를 사용하면 요소의 크기, 모양 및 색상을 변경하는 옵션을 사용하여 플롯의 모양을 쉽게 사용자 정의할 수 있습니다.

# 예
다음 예는 Seaborn을 사용하여 간단한 산점도를 만드는 방법을 보여줍니다.

```py
import seaborn as sns
import matplotlib.pyplot as plt

# Create a dataset
x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]

# Create a scatter plot
sns.scatterplot(x, y, color='blue')

# Show the plot
plt.show()
```

# 장점과 단점
Seaborn은 매력적이고 유익한 통계 그래픽을 만들기 위한 강력하고 사용하기 쉬운 라이브러리입니다. 최소한의 노력으로 매력적인 시각화를 신속하게 생성할 수 있는 다양한 기능을 제공합니다. 또한 라이브러리를 사용하면 요소의 크기, 모양 및 색상을 변경하는 옵션을 사용하여 플롯의 모양을 쉽게 사용자 정의할 수 있습니다.

그러나 Seaborn은 ggplot2 또는 plotly와 같은 다른 데이터 시각화 라이브러리만큼 강력하지 않습니다. 또한 matplotlib와 같은 다른 라이브러리만큼 사용자 친화적이지 않습니다.

# 관련 기술
Seaborn은 matplotlib 및 pandas와 밀접하게 통합되어 있습니다. Matplotlib는 데이터 시각화를 생성하기 위한 강력한 저수준 라이브러리인 반면 pandas는 강력한 데이터 분석 라이브러리입니다.

# 기타
Seaborn은 오픈 소스 라이브러리로 BSD 라이선스로 출시되었습니다. 자원 봉사 팀이 적극적으로 개발하고 유지 관리합니다.