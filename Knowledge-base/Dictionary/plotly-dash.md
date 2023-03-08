---
title: Plotly Dash
description: 
published: true
date: 2023-02-11T14:17:41.754Z
tags: 
editor: markdown
dateCreated: 2023-02-11T14:17:39.880Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Plotly Dash***English** document is available*](/en/Knowledge-base/Dictionary/plotly-dash)
{.links-list}


# 개요
Plotly Dash는 대화형 웹 애플리케이션을 만들기 위한 오픈 소스 Python 라이브러리입니다. 인기 있는 Plotly 라이브러리 위에 구축되어 사용자가 고도로 사용자 지정 가능한 대화형 데이터 시각화를 만들 수 있습니다. Dash는 데이터 과학자, 개발자 및 분석가가 강력한 데이터 기반 애플리케이션을 만드는 데 사용합니다.

# 설명
Plotly Dash는 Python으로 대화형 웹 애플리케이션을 만들기 위한 라이브러리입니다. 인기 있는 Plotly 라이브러리 위에 구축되어 사용자가 고도로 사용자 지정 가능한 대화형 데이터 시각화를 만들 수 있습니다. Dash는 데이터 과학자, 개발자 및 분석가가 강력한 데이터 기반 애플리케이션을 만드는 데 사용합니다. Dash 응용 프로그램은 웹 응용 프로그램 프런트 엔드와 응용 프로그램을 실행하는 Python 코드의 두 부분으로 구성됩니다. 웹 애플리케이션 프런트 엔드는 HTML, CSS 및 JavaScript로 작성되며 데이터 시각화 표시를 담당합니다. Python 코드는 데이터 시각화 생성을 담당하며 Python으로 작성됩니다.

Dash 응용 프로그램은 고도로 사용자 지정이 가능하고 대화식입니다. Dash를 사용하면 확대/축소, 패닝 및 호버링과 같은 다양한 대화형 기능을 사용하여 데이터 시각화를 만들 수 있습니다. Dash는 또한 선 차트, 막대 차트, 산점도 등을 포함하여 다양한 차트와 플롯을 제공합니다.

# 특징
Plotly Dash는 Python으로 대화형 웹 애플리케이션을 만들기 위한 다양한 기능을 제공합니다. 일부 기능은 다음과 같습니다.

- 꺾은선형 차트, 막대형 차트, 산점도 등을 포함한 다양한 차트 및 플롯.
- 확대/축소, 패닝 및 호버링과 같은 기능을 사용하여 고도로 사용자 지정 가능한 대화형 데이터 시각화.
- Pandas, SciPy 및 NumPy와 같은 다른 Python 라이브러리와 쉽게 통합됩니다.
- Dash 애플리케이션을 웹에 쉽게 배포합니다.

# 예
다음은 선형 차트를 표시하는 간단한 대시 애플리케이션의 예입니다.

```python
import dash
import dash_core_components as dcc
import dash_html_components as html
import plotly.graph_objects as go

app = dash.Dash()

app.layout = html.Div([
    dcc.Graph(
        figure=go.Figure(
            data=[
                go.Scatter(
                    x=[1, 2, 3],
                    y=[4, 5, 6],
                    mode='lines'
                )
            ]
        )
    )
])

if __name__ == '__main__':
    app.run_server(debug=True)
```

# 장점과 단점
장점:

- 사용하기 쉽고 고도로 사용자 정의할 수 있습니다.
- 다양한 차트와 플롯.
- 다른 Python 라이브러리와 쉽게 통합됩니다.
- 웹에 애플리케이션을 쉽게 배포합니다.

단점:

- 크고 복잡한 응용 프로그램에는 적합하지 않습니다.
- JavaScript 및 HTML과 같은 다른 언어에 대한 제한된 지원.

# 관련 기술
Plotly Dash는 Plotly, Bokeh 및 Matplotlib와 같은 다른 라이브러리와 관련이 있습니다. 이러한 라이브러리는 모두 Python에서 데이터 시각화를 만드는 데 사용됩니다. Plotly와 Dash는 둘 다 인기 있는 Plotly 라이브러리를 기반으로 구축되었으며 사용자가 고도로 사용자 지정 가능한 대화형 데이터 시각화를 만들 수 있도록 합니다. Bokeh는 Python으로 대화형 데이터 시각화를 만들기 위한 라이브러리이며 대화형 웹 애플리케이션을 만드는 데 사용됩니다. Matplotlib는 Python으로 정적 데이터 시각화를 생성하기 위한 라이브러리이며 정적 데이터 시각화를 생성하는 데 사용됩니다.