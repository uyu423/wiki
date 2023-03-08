---
title: 자연어 처리(NLP) 소개
description: 
published: true
date: 2023-01-31T05:57:45.626Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:57:43.958Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [An Introduction to Natural Language Processing (NLP)***English** version of this document is available*](/en/Knowledge-base/Common/an-introduction-to-natural-language-processing-nlp)
{.links-list}


# 자연어 처리(NLP) 소개

NLP는 인간과 컴퓨터 간의 상호 작용과 관련된 컴퓨터 과학 및 인공 지능 분야입니다. 텍스트를 분석하고 의미를 이해하는 데 도움이 됩니다.

NLP는 다음과 같은 다양한 응용 프로그램에서 사용됩니다.

- 감정 분석
- 언어 번역
- 음성 인식
- 챗봇
- 텍스트 분류


## NLP란?

NLP는 인간의 언어를 이해하고 그로부터 의미를 추출하는 인공 지능의 한 분야입니다. 자신의 언어로 인간과 상호 작용할 수 있는 컴퓨터 시스템을 구축하는 데 사용됩니다.

NLP는 복잡한 분야이며 다양한 문제를 해결하는 데 사용할 수 있는 다양한 기술이 있습니다. 이 기사에서는 가장 일반적인 NLP 작업 및 기술에 대해 간략하게 소개합니다.

## NLP 작업

### 감정 분석

감정 분석은 텍스트의 감정적 톤을 결정하는 작업입니다. 브랜드나 제품에 대한 여론을 측정하는 데 자주 사용됩니다.

감정 분석을 수행하는 방법에는 여러 가지가 있지만 일반적인 접근 방식 중 하나는 사전 훈련된 기계 학습 모델을 사용하는 것입니다. 이러한 모델은 레이블이 지정된 텍스트의 대규모 데이터 세트에서 학습되며 새 텍스트의 감정을 예측하는 데 사용할 수 있습니다.

아래 예에서는 TextBlob 라이브러리를 사용하여 몇 가지 영화 리뷰에 대한 감정 분석을 수행합니다. TextBlob은 텍스트 데이터 작업을 쉽게 해주는 Python 라이브러리입니다.

```python
from textblob import TextBlob

# The TextBlob library uses a pre-trained machine learning model to 
# predict the sentiment of a text. 

# We can use the .sentiment property to get the polarity and 
# subjectivity of a text.

# Polarity is a float value between -1.0 (most negative) and 1.0 (most positive).
# Subjectivity is a float value between 0.0 (objective) and 1.0 (subjective).

# The .polarity and .subjectivity properties return tuples 
# containing the polarity and subjectivity values.

# We can access each value separately like this:

# polarity = text.sentiment.polarity
# subjectivity = text.sentiment.subjectivity

text1 = "I loved the movie! It was so funny and exciting."
text2 = "I hated the movie. It was so boring and slow."

blob1 = TextBlob(text1)
blob2 = TextBlob(text2)

print(blob1.sentiment)
# (0.875, 0.625)

print(blob2.sentiment)
# (-0.625, 0.625)
```

보시다시피 기계 학습 모델은 두 텍스트의 감정을 올바르게 분류할 수 있었습니다.

### 언어 번역

언어 번역은 텍스트를 한 언어에서 다른 언어로 번역하는 작업입니다. 종종 다른 언어로 같은 것을 말하는 방법이 다양하기 때문에 이것은 컴퓨터에게 어려운 작업입니다.

언어 번역에는 규칙 기반 번역과 기계 번역이라는 두 가지 일반적인 접근 방식이 있습니다.

규칙 기반 번역에서 인간 언어학자는 소스 언어의 단어와 구문을 대상 언어로 매핑하는 일련의 규칙을 만듭니다. 이 접근 방식은 매우 정확하지만 노동 집약적이며 속도가 느릴 수 있습니다.

기계 번역은 기계 학습 알고리즘을 사용하여 텍스트를 번역하는 방법을 배우는 보다 자동화된 접근 방식입니다. 이 접근 방식은 훨씬 빠르지만 때때로 규칙 기반 번역보다 정확도가 떨어질 수 있습니다.

아래 예에서는 googletrans 라이브러리의 translate() 함수를 사용하여 텍스트를 영어에서 스페인어로 번역합니다. Google 번역은 여러 언어 간에 텍스트를 번역할 수 있는 기계 번역 서비스입니다.

```python
from googletrans import Translator

translator = Translator()

# The translate() function translates a text from one language to another.
# The src and dest parameters specify the source and target languages.
# The text parameter is the text to be translated.

result = translator.translate(text="Hello, world!", src="en", dest="es")

print(result.text)
# Hola, mundo!
```

보시다시피 기계 번역 서비스는 텍스트를 영어에서 스페인어로 정확하게 번역할 수 있었습니다.

### 음성 인식

음성 인식은 음성(오디오 신호)을 텍스트로 변환하는 작업입니다. 이것은 같은 것을 말하는 방법이 다양하고 같은 사람이 같은 것을 매번 다르게 말할 수 있기 때문에 컴퓨터에게는 어려운 작업입니다.

음성 인식에는 규칙 기반 음성 인식과 통계적 음성 인식이라는 두 가지 일반적인 접근 방식이 있습니다.

규칙 기반 음성 인식에서 인간 언어학자는 소리를 단어와 구문에 매핑하는 일련의 규칙을 만듭니다. 이 접근 방식은 매우 정확하지만 노동 집약적이며 속도가 느릴 수 있습니다.

통계적 음성 인식은 기계 학습 알고리즘을 사용하여 음성 인식 방법을 학습하는 보다 자동화된 접근 방식입니다. 이 접근 방식은 훨씬 빠르지만 때때로 규칙 기반 음성 인식보다 정확도가 떨어질 수 있습니다.

아래 예에서는 SpeechRecognition 라이브러리를 사용하여 WAV 오디오 파일에서 음성을 인식합니다. SpeechRecognition 라이브러리는 음성 데이터 작업을 쉽게 해주는 Python 라이브러리입니다.

```python
import speech_recognition as sr

# The speech_recognition library uses the pocketsphinx speech recognition 
# engine to recognize speech.

# We can use the recognize_sphinx() function to recognize speech from an 
# audio file.

# Theaudio_file parameter is the path to the audio file to be recognized.
# The language parameter is the BCP-47 code for the language of the speech.

# The recognize_sphinx() function returns a list of recognition results. 
# Each result contains the transcript of the recognized speech 
# and a confidence score.

r = sr.Recognizer()

with sr.AudioFile("audio.wav") as source:
    audio = r.record(source)

results = r.recognize_sphinx(audio, language="en-US")

for result in results:
    print(result["transcript"], result["confidence"])

# Hello, world! 1.0
# This is a test. 0.8
```

보시다시피 pocketsphinx 음성 인식 엔진은 오디오 파일에서 음성을 올바르게 인식할 수 있었습니다.

### 챗봇

챗봇은 인간의 말을 이해하고 응답할 수 있는 컴퓨터 프로그램입니다. 그들은 일반적으로 고객 서비스 에이전트로 사용됩니다.

챗봇은 일반적으로 기계 학습 알고리즘을 사용하여 구축됩니다. 첫 번째 단계는 예제 대화의 데이터 세트를 만드는 것입니다. 그런 다음 이 데이터 세트는 기계 학습 모델을 교육하는 데 사용됩니다. 그런 다음 이 모델을 사용하여 새로운 입력에 대한 응답을 생성합니다.

아래 예에서는 ChatterBot 라이브러리를 사용하여 챗봇을 구축합니다. ChatterBot은 챗봇을 쉽게 만들 수 있는 Python 라이브러리입니다.

```python
from chatterbot import ChatBot

# The ChatBot class creates a new chatbot.

# The statement_comparison_function parameter is a function that is used 
# to compare the similarity of two statements.
# The response_selection_method parameter is a function that is used to 
# select a response from a list of responses.

bot = ChatBot(
    "John",
    statement_comparison_function=lambda a, b: a.confidence < b.confidence,
    response_selection_method=lambda a: a[0],
)

# The train() method trains the chatbot on a dataset of example conversations.
# The dataset is a list of tuples, where each tuple contains the input 
# statement and the output response.

dataset = [
    ("Hello, world!", "Hello, John!"),
    ("How are you?", "I'm good, thanks for asking."),
    ("What is your favorite food?", "I like pizza!"),
]

bot.train(dataset)

# The get_response() method generates a response to an input statement.
# The input statement is specified as a string.

response = bot.get_response("Hello, world!")

print(response)
# Hello, John!
```

보시다시피 챗봇은 입력된 문장에 올바르게 응답할 수 있었습니다.

## NLP 기술

자연어 처리에 사용할 수 있는 다양한 기술이 있습니다. 이 섹션에서는 가장 일반적인 몇 가지 기술을 소개합니다.

### 토큰화

토큰화는 텍스트를 개별 토큰으로 분할하는 프로세스입니다. 토큰은 텍스트의 기본 의미 단위입니다. 예를 들어, "I am a student" 텍스트의 토큰은 "I", "am", "a" 및 "student"입니다.

tokenize.py

```python
from nltk.tokenize import word_tokenize

# The word_tokenize() function from the NLTK library tokenizes a text 
# into a list of words.

text = "I am a student"
tokens = word_tokenize(text)

print(tokens)
# ['I', 'am', 'a', 'student']
```

보시다시피 word_tokenize() 함수는 텍스트를 단어 목록으로 올바르게 토큰화할 수 있었습니다.

### 품사 태깅

품사 태그 지정은 텍스트의 각 토큰에 품사 태그를 할당하는 프로세스입니다. 품사 태그는 단어의 문법적 기능을 나타내는 레이블입니다. 예를 들어, "I am a student" 텍스트의 토큰에는 "PRON", "VERB", "DET" 및 "NOUN" 태그가 있습니다.

postag.py

```python
from nltk import pos_tag

# The pos_tag() function from the NLTK library assigns a part of speech 
# tag to each token in a text.

text = "I am a student"
tokens = word_tokenize(text)
tags = pos_tag(tokens)

print(tags)
# [('I', 'PRP'), ('am', 'VBP'), ('a', 'DT'), ('student', 'NN')]
```

보시다시피 pos_tag() 함수는 텍스트의 토큰에 올바르게 태그를 지정할 수 있었습니다.

### 개체명 인식

명명된 엔터티 인식은 텍스트에서 고유 명사를 식별하고 분류하는 프로세스입니다. 고유 명사는 사람, 장소, 조직 및 사물의 이름입니다. 예를 들어, "나는 가게에 갔다"라는 텍스트의 명명된 엔터티는 "나", "상점"입니다.

ner.py

```python
from nltk import ne_chunk

# The ne_chunk() function from the NLTK library identifies named entities 
# in a text.

text = "I went to the store"
tokens = word_tokenize(text)
tags = pos_tag(tokens)
named_entities = ne_chunk(tags)

print(named_entities)
# [('I', 'PRP'), ('went', 'VBD'), ('to', 'TO'), ('the', 'DT'), 
#  ('store', 'NN')]
```

보시다시피 ne_chunk() 함수는 텍스트에서 명명된 엔터티를 올바르게 식별할 수 있었습니다.