---
title: Numpy
description: 
published: true
date: 2023-01-31T06:36:42.034Z
tags: 
editor: markdown
dateCreated: 2023-01-31T06:36:40.420Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Numpy***English** version of this document is available*](/en/Knowledge-base/Dictionary/numpy)
{.links-list}

  
# 개요
Numpy는 Python의 과학 컴퓨팅에 사용되는 오픈 소스 라이브러리입니다. 데이터 분석 및 조작을 위한 강력한 도구이며 빠른 실행 속도, 객체 지향 프로그래밍 및 강력한 데이터 구조와 같은 많은 유용한 기능을 제공합니다. Numpy는 데이터 분석에서 기계 학습, 과학 컴퓨팅에 이르기까지 다양한 작업에 사용할 수 있습니다.

# 역사
Numpy는 2006년 Travis Oliphant에 의해 만들어졌습니다. 과학 컴퓨팅을 위한 오픈 소스 라이브러리인 SciPy 라이브러리의 일부로 개발되었습니다. Numpy는 생성 이후 인기가 높아졌으며 현재 전 세계의 데이터 과학자, 기계 학습 엔지니어 및 소프트웨어 개발자가 일상적으로 사용하고 있습니다.

# 설명
Numpy는 Python에서 숫자 데이터를 빠르고 효율적으로 조작할 수 있는 강력한 라이브러리입니다. 다음과 같은 많은 유용한 기능을 제공합니다.

* **배열 객체**: Numpy는 동일한 유형의 여러 요소를 보유할 수 있는 배열 객체를 제공합니다. 배열을 사용하여 많은 양의 데이터를 빠르고 효율적으로 저장하고 조작할 수 있습니다.

* **수학 함수**: Numpy는 배열에서 수학 연산을 수행하는 데 사용할 수 있는 많은 수학 함수를 제공합니다. 이러한 함수에는 덧셈, 뺄셈, 곱셈 및 나눗셈과 같은 기본 수학 연산과 행렬 곱셈, 푸리에 변환 및 선형 대수 연산과 같은 고급 함수가 포함됩니다.

* **객체 지향 프로그래밍**: Numpy는 데이터 조작에 대한 객체 지향 접근 방식을 제공하므로 사용과 이해가 쉽습니다. 개체, 클래스 및 함수를 사용하여 데이터를 조작하고 분석할 수 있습니다.

# 예
데이터 포인트의 2차원 배열이 있다고 가정해 보겠습니다. Numpy를 사용하여 다음 코드를 사용하여 배열의 각 행의 평균을 쉽게 계산할 수 있습니다.

```python
import numpy as np

# Create a 2D array 
data = np.array([[1,2,3],
                 [4,5,6],
                 [7,8,9]])

# Calculate the average of each row
row_means = np.mean(data, axis=1)

# Print the result
print(row_means)

# Output: [2. 5. 8.]
```

# 장점과 단점
Numpy는 효율적인 데이터 분석 및 조작을 가능하게 하는 강력하고 유연한 라이브러리입니다. 다음과 같은 많은 이점이 있습니다.

* **속도**: Numpy는 고도로 최적화되어 대부분의 다른 라이브러리보다 빠르게 실행할 수 있습니다.

* **객체 지향 프로그래밍**: Numpy의 객체 지향 접근 방식을 사용하면 쉽게 사용하고 이해할 수 있습니다.

* **다양한 기능**: Numpy는 복잡한 계산을 쉽게 수행할 수 있도록 다양한 수학 함수를 제공합니다.

그러나 Numpy에는 다음과 같은 몇 가지 단점도 있습니다.

* **일부 데이터 유형에 대한 지원 부족**: Numpy는 개체 및 문자열과 같은 일부 데이터 유형을 지원하지 않습니다.

* **제한된 문서**: Numpy는 좋은 문서를 제공하지만 범위가 제한되어 있고 항상 명확하거나 이해하기 쉽지 않을 수 있습니다.

# 관련된 링크들
- [Numpy (영어) *공식 사이트*](https://numpy.org/)
- [Numpy 튜토리얼(영문) *Real Python*](https://realpython.com/numpy-tutorial-python/)
- [NumPy 튜토리얼(독일어) *Python Academy*](https://www.python-academy.com/python_numpy_tutorial.html)
{.links-list}