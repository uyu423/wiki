---
title: Bokeh
description: 
published: true
date: 2023-02-01T10:37:59.361Z
tags: 
editor: markdown
dateCreated: 2023-02-01T10:37:56.016Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}

- [Bokeh***English** version of this document is available*](/en/Knowledge-base/Dictionary/bokeh)
{.links-list}

# 개요

Bokeh는 사용자가 정교하고 강력한 데이터 시각화를 만들 수 있도록 하는 Python용 대화형 시각화 라이브러리입니다. 데이터 탐색 및 분석을 위한 강력한 도구이며 효과적이고 의미 있는 방식으로 데이터를 분석하고 표시해야 하는 데이터 과학자, 통계학자 및 기타 전문가가 사용합니다. Bokeh는 Jupyter 노트북 및 기타 대화형 도구와 함께 사용하도록 설계되었으며 다양한 기능을 제공합니다.

# 설명

Bokeh는 사용자가 정교하고 강력한 데이터 시각화를 만들 수 있도록 하는 Python용 대화형 시각화 라이브러리입니다. 데이터 탐색 및 분석을 위한 강력한 도구이며 효과적이고 의미 있는 방식으로 데이터를 분석하고 표시해야 하는 데이터 과학자, 통계학자 및 기타 전문가가 사용합니다. Bokeh는 Jupyter 노트북 및 기타 대화형 도구와 함께 사용하도록 설계되었으며 다양한 기능을 제공합니다.

Bokeh는 대화형 데이터 시각화를 만들기 위한 고급 인터페이스를 제공하는 라이브러리입니다. 인기 있는 플로팅 라이브러리 Matplotlib 위에 구축되었으며 대화형 시각화를 보다 쉽게 만들 수 있는 여러 기능을 제공합니다. Bokeh는 Jupyter 노트북 및 기타 대화형 도구와 함께 사용하도록 설계되었으며 다양한 기능을 제공합니다.

Bokeh는 선 차트, 막대 차트, 산점도, 히스토그램 등 다양한 유형의 시각화를 제공합니다. 또한 필터링, 정렬 및 확대/축소와 같은 데이터 조작 및 탐색을 위한 다양한 도구를 제공합니다. 또한 Bokeh는 대화형 슬라이더, 버튼 및 기타 위젯과 같은 대화형 시각화를 만들기 위한 다양한 도구를 제공합니다.

Bokeh는 Jupyter 노트북 및 기타 대화형 도구와 함께 사용하도록 설계되었으며 다양한 기능을 제공합니다. 사용하기 쉽고 대화형 시각화를 보다 쉽게 만들 수 있는 여러 기능을 제공합니다. Bokeh는 또한 NumPy 및 Pandas와 같은 다른 라이브러리와 함께 사용하도록 설계되었으며 강력하고 정교한 시각화를 만드는 데 사용할 수 있습니다.

# 역사

Bokeh는 2012년 Continuum Analytics 팀에서 개발했습니다. 이 팀은 현재 Anaconda의 수석 과학자인 Bryan Van de Ven가 이끌었습니다. Bokeh는 Python용 대화형 시각화 라이브러리로 설계되었으며 인기 있는 플로팅 라이브러리인 Matplotlib를 기반으로 구축되었습니다.

Bokeh는 처음에 2012년에 오픈 소스 프로젝트로 출시되었으며 이후 가장 인기 있는 Python용 시각화 라이브러리 중 하나가 되었습니다. 효과적이고 의미 있는 방식으로 데이터를 분석하고 제시해야 하는 데이터 과학자, 통계학자 및 기타 전문가가 사용합니다.

# 특징

Bokeh는 대화형 데이터 시각화를 만들기 위한 다양한 기능을 제공합니다. Jupyter 노트북 및 기타 대화형 도구와 함께 사용하도록 설계되었으며 다양한 기능을 제공합니다.

Bokeh는 선 차트, 막대 차트, 산점도, 히스토그램 등 다양한 유형의 시각화를 제공합니다. 또한 필터링, 정렬 및 확대/축소와 같은 데이터 조작 및 탐색을 위한 다양한 도구를 제공합니다. 또한 Bokeh는 대화형 슬라이더, 버튼 및 기타 위젯과 같은 대화형 시각화를 만들기 위한 다양한 도구를 제공합니다.

Bokeh는 NumPy 및 Pandas와 같은 다른 라이브러리와 함께 사용하도록 설계되었으며 강력하고 정교한 시각화를 만드는 데 사용할 수 있습니다. 또한 Bokeh 시각화에 HTML 및 JavaScript 코드를 포함하는 기능과 같이 대화형 시각화를 보다 쉽게 만들 수 있는 여러 기능을 제공합니다.

# 예

다음은 간단한 Bokeh 시각화의 예입니다. 이 예제에서는 NumPy 및 Pandas 라이브러리를 사용하여 간단한 선 차트를 만듭니다.

```
import numpy as np
import pandas as pd

# Create a dataframe with some random data
df = pd.DataFrame(np.random.randn(10, 4), columns=list('ABCD'))

# Create a Bokeh figure
from bokeh.plotting import figure
p = figure(title="Simple Line Chart")

# Add a line renderer with legend and line thickness
p.line(df.index, df['A'], legend="A", line_width=2)

# Show the results
show(p)
```

# 장점과 단점

Bokeh는 강력하고 정교한 Python용 시각화 라이브러리입니다. 대화형 데이터 시각화를 만들기 위한 다양한 기능을 제공합니다. 그러나 Bokeh를 사용하는 데는 몇 가지 단점이 있습니다.

장점:

- 사용하기 쉽고 대화형 데이터 시각화를 만들기 위한 다양한 기능을 제공합니다.
- NumPy 및 Pandas와 같은 다른 라이브러리와 함께 사용하도록 설계되었으며 강력하고 정교한 시각화를 만드는 데 사용할 수 있습니다.
- 필터링, 정렬 및 확대/축소와 같은 데이터 조작 및 탐색을 위한 다양한 도구를 제공합니다.

단점:

- Python 및 기타 프로그래밍 언어에 익숙하지 않은 사용자는 배우고 사용하기 어려울 수 있습니다.
- 디버그 및 문제 해결이 어려울 수 있습니다.
- Matplotlib와 같은 다른 시각화 라이브러리만큼 널리 사용되지 않습니다.