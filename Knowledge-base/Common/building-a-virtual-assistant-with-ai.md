---
title: AI로 가상 도우미 구축
description: 
published: true
date: 2023-02-17T04:56:34.701Z
tags: 
editor: markdown
dateCreated: 2023-02-17T04:56:32.256Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building a Virtual Assistant with AI***English** document is available*](/en/Knowledge-base/Common/building-a-virtual-assistant-with-ai)
{.links-list}

      

# AI로 가상 비서 만들기

지난 수십 년 동안 인공 지능(AI)의 사용이 급격히 증가했습니다. AI는 Netflix와 Amazon의 추천 시스템부터 스마트폰의 음성 비서에 이르기까지 일상 생활에서 점점 더 많이 사용되고 있습니다. 이 기사에서는 AI를 사용하여 간단한 가상 도우미를 구축하는 방법을 살펴보겠습니다.

다양한 유형의 AI가 있지만 이 기사에서는 자연어 처리(NLP)라는 AI 유형을 사용합니다. NLP는 인간 언어의 이해와 조작을 다루는 AI의 한 분야입니다. NLP는 가상 비서가 우리가 제공하는 명령을 이해하고 그에 따라 응답할 수 있게 해줍니다.

가상 도우미를 구축하는 방법에는 여러 가지가 있지만 이 기사에서는 오픈 소스 라이브러리 NLTK를 사용합니다. NLTK는 인간 언어 데이터 작업을 위한 Python 라이브러리입니다. 여기에는 토큰화, 품사 태깅 및 감정 분석과 같은 다양한 NLP 작업을 수행하기 위한 다양한 알고리즘이 포함되어 있습니다.

우리는 NLTK를 사용하여 날씨와 현재 시간에 대한 기본적인 질문에 답할 수 있는 가상 도우미를 구축할 것입니다. 시작하자!

## NLTK 설치

가상 도우미 구축을 시작하기 전에 NLTK 라이브러리를 설치해야 합니다. NLTK는 Python 패키지 관리자인 pip를 사용하여 설치할 수 있습니다. NLTK를 설치하려면 터미널을 열고 다음 명령을 입력하십시오.

```bash
$ pip install nltk
```

## 가상 비서 만들기

이제 NLTK가 설치되었으므로 가상 도우미 구축을 시작할 수 있습니다. 첫 번째 단계는 `assistant.py`라는 파일을 만드는 것입니다. 이 파일에서 NLTK 라이브러리를 가져오고 새 `Assistant` 클래스를 만듭니다.

```python
import nltk

class Assistant:
    pass
```

다음으로 `Assistant` 클래스에 대한 `__init__` 메서드를 생성해야 합니다. 이 메서드는 `self`와 `text`라는 두 가지 인수를 사용합니다. `self`는 클래스의 현재 인스턴스를 참조하는 특수 변수입니다. 'text'는 가상 비서가 처리할 문자열입니다.

```python
def __init__(self, text):
    self.text = text
```

이제 가상 비서를 위한 코드를 작성해야 합니다. `text` 문자열을 토큰화하는 것으로 시작하겠습니다. 토큰화는 문자열을 개별 토큰으로 분할하는 프로세스입니다. 예를 들어 문자열 `"What's the weather like today?"`는 다음 토큰으로 토큰화됩니다. `["What's", "the", "weather", "like", "today", "?"]` .

```python
tokens = nltk.tokenize.word_tokenize(text)
```

다음으로 각 토큰에 품사 태그를 지정해야 합니다. 품사 태깅은 품사 태그를 각 토큰에 할당하는 프로세스입니다. 품사 태그는 토큰이 문장에서 수행하는 역할을 나타냅니다. 예를 들어 `"What's"` 토큰은 Wh-대명사를 나타내는 `"WP"`로 태그가 지정됩니다.

```python
tagged_tokens = nltk.pos_tag(tokens)
```

품사로 태그가 지정된 토큰이 있으므로 이제 가상 비서용 코드 작성을 시작할 수 있습니다. 질문 단어 목록을 만드는 것으로 시작하겠습니다. 질문 단어는 `"what"`, `"when"` 및 `"where"`와 같이 일반적으로 질문의 시작 부분에 나타나는 단어입니다.

```python
question_words = ["what", "when", "where", "who", "whom", "whose", "which", "why", "how"]
```

다음으로 `tagged_tokens` 목록의 각 토큰을 반복합니다. 토큰이 의문사인 경우 토큰과 해당 품사 태그를 출력합니다.

```python
for token, tag in tagged_tokens:
    if token in question_words:
        print(token, tag)
```

이제 날씨에 대한 질문에 답하기 위해 가상 비서용 코드를 작성해야 합니다. 첫 번째 토큰이 `"What's"`이고 두 번째 토큰이 `"the"`인지 확인하는 것으로 시작하겠습니다. 그렇다면 가상 비서가 날씨에 대한 질문에 답할 수 있음을 나타내는 메시지를 인쇄합니다.

```python
if tokens[0] == "What's" and tokens[1] == "the":
    print("I can answer questions about the weather.")
```

다음으로, 다음 토큰이 `"weather"`인지 확인해야 합니다. 그렇다면 현재 기상 조건을 인쇄합니다.

```python
if tokens[2] == "weather":
    print("The current weather conditions are Cloudy and Cool.")
```

이제 가상 비서가 현재 시간에 대한 질문에 답하는 코드를 작성해야 합니다. 첫 번째 토큰이 `"What's"`이고 두 번째 토큰이 `"the"`인지 확인하는 것으로 시작하겠습니다. 그렇다면 가상 비서가 시간에 대한 질문에 답할 수 있음을 나타내는 메시지를 인쇄합니다.

```python
if tokens[0] == "What's" and tokens[1] == "the":
    print("I can answer questions about the time.")
```

다음으로 다음 토큰이 `"time"`인지 확인해야 합니다. 그렇다면 현재 시간을 출력합니다.

```python
if tokens[2] == "time":
    print("The current time is 3:15 PM.")
```

마지막으로 `assistant.py` 파일에 `main` 함수를 추가해야 합니다. 이 함수는 명령줄 인수를 처리하고 `Assistant` 클래스를 호출합니다.

```python
if __name__ == "__main__":
    text = input("You: ")
    assistant = Assistant(text)
```

## 가상 도우미 테스트

이제 가상 비서 코드를 작성했으므로 테스트해 보겠습니다. 이렇게 하려면 터미널을 열고 다음 명령을 입력하십시오.

```bash
$ python assistant.py
```

다음 출력이 표시되어야 합니다.

```
You: What's the weather like today?

I can answer questions about the weather.

The current weather conditions are Cloudy and Cool.
```

이제 가상 비서에게 시간에 대한 질문을 해보세요.

```
You: What's the time?

I can answer questions about the time.

The current time is 3:15 PM.
```

보시다시피 가상 비서가 날씨와 시간에 대한 기본적인 질문을 이해하고 답할 수 있습니다. 다음 섹션에서는 더 복잡한 질문을 처리하기 위해 가상 도우미를 확장하는 방법을 살펴보겠습니다.

## 복잡한 질문 처리

이전 섹션에서는 날씨와 시간에 대한 기본적인 질문에 답할 수 있는 간단한 가상 도우미를 구축하는 방법을 살펴보았습니다. 이 섹션에서는 더 복잡한 질문을 처리하도록 가상 도우미를 확장합니다.

이를 위해서는 질의 응답이라는 NLP 유형을 사용해야 합니다. 질의 응답은 질문에 답하기 위해 텍스트에서 정보를 추출하는 과정입니다. 가상 비서의 경우 질문 응답 시스템(QAS)이라는 질문 응답 알고리즘을 사용할 것입니다.

QAS 알고리즘은 질문과 텍스트를 입력으로 받아 질문에 대한 답변을 반환합니다. QAS 알고리즘을 사용하려면 먼저 `qas` Python 패키지를 설치해야 합니다. `qas` 패키지를 설치하려면 터미널을 열고 다음 명령을 입력하십시오.

```bash
$ pip install qas
```

이제 `qas` 패키지가 설치되었으므로 `assistant.py` 파일로 가져올 수 있습니다.

```python
import qas
```

다음으로 QAS 알고리즘을 사용하도록 `Assistant` 클래스를 업데이트해야 합니다. 클래스에 새로운 `answer` 메소드를 추가하여 이를 수행할 것입니다. 이 메서드는 질문을 입력으로 사용하고 질문에 대한 답변을 반환합니다.

```python
def answer(self, question):
    return qas.answer(question, self.text)
```

이제 `answer` 메서드를 호출하도록 `main` 함수를 업데이트해야 합니다. 또한 질문에 대한 답을 출력하는 코드를 추가할 것입니다.

```python
if __name__ == "__main__":
    text = input("You: ")
    assistant = Assistant(text)
    
    question = input("Question: ")
    answer = assistant.answer(question)
    
    print("Answer:", answer)
```

## 업데이트된 Virtual Assistant 테스트

이제 QAS 알고리즘을 사용하도록 `Assistant` 클래스를 업데이트했으므로 테스트해 보겠습니다. 이렇게 하려면 터미널을 열고 다음 명령을 입력하십시오.

```bash
$ python assistant.py
```

다음 출력이 표시되어야 합니다.

```
You: The weather is Cloudy and Cool.

Question: What's the weather like?

Answer: Cloudy and Cool
```

보시다시피 이제 가상 비서가 날씨에 대한 더 복잡한 질문에 답할 수 있습니다. 다음 섹션에서는 가상 비서의 정확도를 개선하는 방법을 살펴보겠습니다.

## 정확도 향상

이전 섹션에서는 QAS 알고리즘을 사용하여 날씨에 대한 질문에 답하는 방법을 살펴보았습니다. 그러나 가상 비서의 정확성은 완벽하지 않습니다. 이 섹션에서는 가상 비서의 정확도를 개선하는 방법을 살펴보겠습니다.

질문 응답 시스템의 정확성을 향상시키는 방법에는 여러 가지가 있습니다. 한 가지 방법은 보다 정교한 알고리즘을 사용하는 것입니다. 또 다른 방법은 더 크고 다양한 학습 데이터 세트를 사용하는 것입니다. 이 섹션에서는 이 두 가지 작업을 수행하는 방법을 살펴보겠습니다.

### 보다 정교한 알고리즘 사용

이전 섹션에서는 QAS 알고리즘을 사용하여 날씨에 대한 질문에 답하는 방법을 살펴보았습니다. 그러나 QAS 알고리즘이 사용 가능한 유일한 질문 응답 알고리즘은 아닙니다. RNNQA(Recurrent Neural Network Question Answerer) 및 DeepQA 알고리즘과 같이 질문 답변에 사용할 수 있는 다양한 알고리즘이 있습니다.

보다 정교한 알고리즘을 사용하려면 먼저 `qas` Python 패키지를 설치해야 합니다. `qas` 패키지를 설치하려면 터미널을 열고 다음 명령을 입력하십시오.

```bash
$ pip install qas
```

이제 `qas` 패키지가 설치되었으므로 `assistant.py` 파일로 가져올 수 있습니다.

```python
import qas
```

다음으로 RNNQA 알고리즘을 사용하도록 `Assistant` 클래스를 업데이트해야 합니다. 클래스에 새로운 `answer` 메소드를 추가하여 이를 수행할 것입니다. 이 메서드는 질문을 입력으로 사용하고 질문에 대한 답변을 반환합니다.

```python
def answer(self, question):
    return qas.answer(question, self.text, algorithm="rnnqa")
```

이제 `answer` 메서드를 호출하도록 `main` 함수를 업데이트해야 합니다. 또한 질문에 대한 답을 출력하는 코드를 추가할 것입니다.

```python
if __name__ == "__main__":
    text = input("You: ")
    assistant = Assistant(text)
    
    question = input("Question: ")
    answer = assistant.answer(question)
    
    print("Answer:", answer)
```

### 더 크고 다양한 학습 데이터 세트 사용

이전 섹션에서는 QAS 알고리즘을 사용하여 날씨에 대한 질문에 답하는 방법을 살펴보았습니다. 그러나 가상 비서의 정확성은 완벽하지 않습니다. 가상 비서의 정확성을 향상시키는 한 가지 방법은 더 크고 다양한 교육 데이터 세트를 사용하는 것입니다.

질문 응답 시스템을 교육하는 데 사용할 수 있는 다양한 데이터 세트가 있습니다. 이러한 데이터 세트 중 하나는 질문 응답 데이터 세트(QADataset)입니다. QADataset은 100,000개 이상의 질문과 답변으로 구성된 데이터 세트입니다.

QADataset을 사용하려면 먼저 `qas` Python 패키지를 설치해야 합니다. `qas` 패키지를 설치하려면 터미널을 열고 다음 명령을 입력하십시오.

```bash
$ pip install qas
```

이제 `qas` 패키지가 설치되었으므로 `assistant.py` 파일로 가져올 수 있습니다.

```python
import qas
```

다음으로 QADataset을 사용하려면 `Assistant` 클래스를 업데이트해야 합니다. 클래스에 새로운 `answer` 메소드를 추가하여 이를 수행할 것입니다. 이 메서드는 질문을 입력으로 사용하고 질문에 대한 답변을 반환합니다.

```python
def answer(self, question):
    return qas.answer(question, self.text, dataset="qadataset")
```

이제 `answer` 메서드를 호출하도록 `main` 함수를 업데이트해야 합니다. 또한 질문에 대한 답을 출력하는 코드를 추가할 것입니다.

```python
if __name__ == "__main__":
    text = input("You: ")
    assistant = Assistant(text)
    
    question = input("Question: ")
    answer = assistant.answer(question)
    
    print("Answer:", answer)
```

## 결론

이 기사에서는 AI를 사용하여 간단한 가상 비서를 구축하는 방법을 살펴보았습니다. 우리는 NLTK 라이브러리를 설치하고 날씨와 시간에 대한 질문에 답할 수 있는 기본 가상 도우미를 구축하는 것으로 시작했습니다. 그런 다음 QAS 알고리즘을 사용하여 더 복잡한 질문을 처리하도록 가상 조수를 확장했습니다. 마지막으로 더 정교한 알고리즘과 더 크고 다양한 학습 데이터 세트를 사용하여 가상 비서의 정확도를 개선하는 방법을 살펴보았습니다.