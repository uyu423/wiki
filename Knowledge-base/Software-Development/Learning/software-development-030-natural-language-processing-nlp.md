---
title: 소프트웨어 개발 030: 자연어 처리(NLP)
description: 
published: true
date: 2023-02-09T15:56:24.362Z
tags: 
editor: markdown
dateCreated: 2023-02-09T15:56:22.589Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Software Development 030: Natural Language Processing (NLP)***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-030-natural-language-processing-nlp)
{.links-list}


# 소프트웨어 개발 030: 자연어 처리(NLP)

이 게시물에서는 자연어 처리(NLP)에 대해 종합적이고 실용적인 방법을 살펴보겠습니다. NLP가 무엇인지, NLP가 사용되는 일부 작업 및 Python에서 코딩을 시작하는 방법을 다룰 것입니다.

## NLP란?

자연어 처리(NLP)는 컴퓨터와 인간(자연) 언어 사이의 상호 작용, 특히 대량의 자연어 데이터를 처리하고 분석하도록 컴퓨터를 프로그래밍하는 방법과 관련된 컴퓨터 과학 및 인공 지능 분야입니다.

NLP는 챗봇, 자동 음성 인식 및 기계 번역과 같은 애플리케이션을 구축하는 데 사용됩니다.

## NLP 작업

NLP로 수행할 수 있는 다양한 작업이 있습니다. 가장 일반적인 작업 중 일부는 다음과 같습니다.

- **텍스트 분류:** 텍스트에 범주 또는 레이블 지정(예: 스팸 감지, 감정 분석.

- **정보 추출:** 구조화되지 않은 텍스트에서 구조화 데이터를 추출합니다. 문서에서 날짜, 이름 및 위치를 추출합니다.

- **자연어 생성:** 데이터에서 텍스트 생성. 문서 요약 생성.

- **음성 인식:** 음성을 텍스트로 변환, 예: 음성-텍스트 응용 프로그램.

- **기계 번역:** 텍스트를 한 언어에서 다른 언어로 번역합니다. 구글 번역.

## NLP 시작하기

이 섹션에서는 NLP용 Python 코딩의 기본 사항을 다룹니다. 인간 언어 데이터 작업에 널리 사용되는 Python 라이브러리인 NLTK(Natural Language Toolkit)를 사용할 것입니다.

### NLTK 설치

코딩을 시작하기 전에 NLTK를 설치해야 합니다. NLTK는 Python용 패키지 관리자인 pip를 사용하여 설치할 수 있습니다.

```
pip install nltk
```

### NLTK 데이터 다운로드

NLTK가 설치되면 NLTK가 사용할 데이터를 다운로드해야 합니다. 이 데이터에는 영어 단어 목록, 문법 규칙 등이 포함됩니다.

NLTK 다운로더를 사용하여 이 데이터를 다운로드할 수 있습니다.

```python
import nltk

nltk.download()
```

그러면 다운로드할 데이터를 선택할 수 있는 창이 열립니다. 지금은 "인기 있는" 데이터만 다운로드하겠습니다.

### NLTK 기초

이제 NLTK를 설치하고 데이터를 다운로드했으므로 NLTK의 일부 기능을 사용해 볼 수 있습니다.

먼저 NLTK 라이브러리를 가져옵니다.

```python
import nltk
```

다음으로 작업할 텍스트를 선택하겠습니다. NLTK는 우리가 사용할 수 있는 많은 텍스트와 함께 제공됩니다. 이 예에서는 여러 고전 서적을 포함하는 "구텐베르그" 코퍼스를 사용합니다.

```python
from nltk.corpus import gutenberg
```

이제 구텐베르크 말뭉치가 로드되었으므로 포함된 텍스트에 액세스할 수 있습니다. 예를 들어 "Alice's Adventures in Wonderland"라는 텍스트를 얻으려면 다음을 수행할 수 있습니다.

```python
alice = gutenberg.raw('carroll-alice.txt')
```

텍스트의 단어에 액세스할 수도 있습니다.

```python
alice_words = gutenberg.words('carroll-alice.txt')
```

그리고 문장:

```python
alice_sents = gutenberg.sents('carroll-alice.txt')
```

### 텍스트 전처리

텍스트에 대한 추가 분석을 수행하기 전에 사전 처리가 필요합니다. 이 전처리 단계에는 다음이 포함됩니다.

- 토큰화: 텍스트를 개별 단어 또는 문장으로 분할합니다.

- 정규화: 단어를 소문자로 변환하고 구두점을 제거합니다.

- 어간 추출 또는 표제어 추출: 단어를 기본 형태로 줄입니다.

여기에서 이러한 각 단계에 대해 너무 자세히 설명하지는 않지만 NLTK는 이러한 사전 처리 단계를 쉽게 수행할 수 있는 여러 기능을 제공합니다.

예를 들어 텍스트를 문장으로 토큰화하려면 ```sent_tokenize``` 함수를 사용할 수 있습니다.

```python
from nltk.tokenize import sent_tokenize

sentences = sent_tokenize(alice)
```

텍스트를 단어로 토큰화하려면 ```word_tokenize``` 함수를 사용할 수 있습니다.

```python
from nltk.tokenize import word_tokenize

words = word_tokenize(alice)
```

소문자로 변환하고 구두점을 제거하여 텍스트를 정규화할 수도 있습니다.

```python
from nltk.tokenize import RegexpTokenizer

tokenizer = RegexpTokenizer(r'\w+')

words = tokenizer.tokenize(alice.lower())
```

마지막으로 텍스트를 줄기 또는 표제어화할 수 있습니다. 어간 추출은 단어를 기본 형태로 줄입니다. "실행"은 "실행"이 됩니다. 원형 복원은 단어를 기본 형식으로 축소하지만 단어의 문맥을 고려합니다. "running"은 "run"이 되지만 "ran"은 "run"이 됩니다.

```python
from nltk.stem import PorterStemmer, WordNetLemmatizer

stemmer = PorterStemmer()
lemmatizer = WordNetLemmatizer()

stemmed_words = [stemmer.stem(w) for w in words]
lemmatized_words = [lemmatizer.lemmatize(w) for w in words]
```

### 품사 태깅

품사(POS) 태깅은 텍스트의 각 단어에 POS 태그를 할당하는 프로세스입니다. POS 태그는 단어의 문법적 기능을 나타내는 레이블입니다. 단어가 명사, 동사, 형용사 등인지 여부

NLTK는 다양한 POS 태거를 제공하지만 이 예에서는 기본 POS 태거를 사용합니다.

```python
from nltk import pos_tag

tagged_words = pos_tag(words)
```python
positive_words = ['good', 'great', 'awesome', 'fantastic', 'excellent']
negative_words = ['bad', 'terrible', 'horrible', 'awful', 'poor']
```python
from nltk import ne_chunk

named_entities = ne_chunk(tagged_words)
```파이썬
nltk import ne_chunk에서

named_entities = ne_chunk(tagged_words)
```

```ne_chunk``` 함수의 출력은 트리이며 트리의 각 노드는 명명된 엔터티를 나타냅니다.

### 텍스트 분류

텍스트 분류는 범주 또는 레이블을 텍스트에 할당하는 작업입니다. 예를 들어 텍스트를 "긍정적" 또는 "부정적"으로 분류할 수 있습니다.

텍스트 분류에 접근하는 방법에는 여러 가지가 있지만 이 예에서는 간단한 단어 모음 접근 방식을 사용합니다.

먼저 긍정적인 단어와 부정적인 단어의 목록을 만듭니다.

```python
num_positive_words = 0
num_negative_words = 0

for word in words:
    if word in positive_words:
        num_positive_words += 1
    elif word in negative_words:
        num_negative_words += 1
```

다음으로 텍스트에서 긍정적이고 부정적인 단어의 수를 세겠습니다.

```python
if num_positive_words > num_negative_words:
    print('The text is positive.')
elif num_positive_words < num_negative_words:
    print('The text is negative.')
else:
    print('The text is neutral.')
```

마지막으로 긍정 단어와 부정 단어의 수에 따라 텍스트를 긍정 또는 부정으로 분류합니다.

```파이썬
num_positive_words > num_negative_words인 경우:
    print('텍스트가 긍정적입니다.')
elif num_positive_words < num_negative_words:
    print('텍스트가 음수입니다.')
또 다른:
    print('텍스트는 중립적입니다.')
```

물론 이것은 텍스트 분류에 대한 매우 단순한 접근 방식이며 실제로는 더 정교한 방법을 사용합니다.

## 더 읽을 수 있는 리소스

- [Natural Language Processing with Python](http://www.nltk.org/book/) - Python의 NLP에 대한 종합적이고 실용적인 안내서입니다.

- [Python for NLP: Tokenization, Stemming, and Lemmatization](https://www.datacamp.com/community/tutorials/stemming-lemmatization-python) - Python에서 텍스트 전처리를 수행하는 방법에 대한 자습서입니다.

- [NLTK를 사용한 명명된 엔터티 인식](https://towardsdatascience.com/named-entity-recognition-with-nltk-d0a87a1544f1) - NLTK를 사용하여 Python에서 NER을 수행하는 방법에 대한 자습서입니다.

- [NLTK를 사용한 텍스트 분류](https://towardsdatascience.com/text-classification-with-nltk-d0a87a1544f1) - NLTK를 사용하여 Python에서 텍스트 분류를 수행하는 방법에 대한 자습서입니다.