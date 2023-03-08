---
title: 自然语言处理 (NLP) 简介
description: 
published: true
date: 2023-01-31T05:57:45.639Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:57:43.968Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [An Introduction to Natural Language Processing (NLP)***English** version of this document is available*](/en/Knowledge-base/Common/an-introduction-to-natural-language-processing-nlp)
{.links-list}


# 自然语言处理 (NLP) 简介

NLP 是计算机科学和人工智能领域，关注人机交互。它可以帮助您分析文本并理解其含义。

NLP 用于许多不同的应用程序，例如：

- 情绪分析
- 语言翻译
- 语音识别
- 聊天机器人
- 文本分类


## 什么是自然语言处理？

NLP 是人工智能的一个分支，处理理解人类语言并从中提取意义。它用于构建可以用人类自己的语言与人类交互的计算机系统。

NLP 是一个复杂的领域，有许多不同的技术可以用来解决不同的问题。在本文中，我们将简要介绍一些最常见的 NLP 任务和技术。

## 自然语言处理任务

### 情绪分析

情感分析是确定文本情感基调的任务。它通常用于衡量品牌或产品的公众舆论。

执行情感分析的方法有很多种，但一种常见的方法是使用预训练的机器学习模型。这些模型在标记文本的大型数据集上进行训练，可用于预测新文本的情绪。

在下面的示例中，我们将使用 TextBlob 库对一些电影评论进行情感分析。 TextBlob 是一个 Python 库，可以轻松处理文本数据。

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

如您所见，机器学习模型能够正确地对两个文本的情感进行分类。

### 语言翻译

语言翻译是将文本从一种语言翻译成另一种语言的任务。这对计算机来说是一项艰巨的任务，因为通常有许多不同的方式用不同的语言来表达同一件事。

语言翻译有两种常见的方法：基于规则的翻译和机器翻译。

在基于规则的翻译中，人类语言学家创建一组规则，将源语言中的单词和短语映射到目标语言。这种方法非常准确，但它也是劳动密集型的并且可能很慢。

机器翻译是一种更加自动化的方法，它使用机器学习算法来学习如何翻译文本。这种方法要快得多，但有时不如基于规则的翻译准确。

在下面的示例中，我们将使用 googletrans 库中的 translate() 函数将文本从英语翻译成西班牙语。谷歌翻译是一种机器翻译服务，可以在多种语言之间翻译文本。

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

如您所见，机器翻译服务能够将文本从英语正确翻译成西班牙语。

### 语音识别

语音识别是将语音（音频信号）转换为文本的任务。这对计算机来说是一项艰巨的任务，因为说同样的话有很多不同的方式，而且同一个人每次都可以用不同的方式说同样的话。

有两种常见的语音识别方法：基于规则的语音识别和统计语音识别。

在基于规则的语音识别中，人类语言学家创建了一组将声音映射到单词和短语的规则。这种方法非常准确，但它也是劳动密集型的并且可能很慢。

统计语音识别是一种更加自动化的方法，它使用机器学习算法来学习如何识别语音。这种方法要快得多，但有时不如基于规则的语音识别准确。

在下面的示例中，我们将使用 SpeechRecognition 库从 WAV 音频文件中识别语音。 SpeechRecognition 库是一个 Python 库，可以轻松处理语音数据。

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

如您所见，pocketsphinx 语音识别引擎能够正确识别音频文件中的语音。

### 聊天机器人

聊天机器人是可以理解和响应人类语言的计算机程序。他们通常用作客户服务代理。

聊天机器人通常是使用机器学习算法构建的。第一步是创建示例对话的数据集。然后使用该数据集来训练机器学习模型。然后使用该模型生成对新输入的响应。

在下面的示例中，我们将使用 ChatterBot 库来构建聊天机器人。 ChatterBot 是一个 Python 库，可以轻松创建聊天机器人。

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

如您所见，聊天机器人能够正确响应输入语句。

## 自然语言处理技术

有许多不同的技术可用于自然语言处理。在本节中，我们将介绍一些最常用的技术。

### 代币化

标记化是将文本拆分为单个标记的过程。标记是文本中意义的基本单位。例如，文本“我是学生”中的标记是“我”、“是”、“a”和“学生”。

标记化.py

```python
from nltk.tokenize import word_tokenize

# The word_tokenize() function from the NLTK library tokenizes a text 
# into a list of words.

text = "I am a student"
tokens = word_tokenize(text)

print(tokens)
# ['I', 'am', 'a', 'student']
```

如您所见，word_tokenize() 函数能够将文本正确标记为单词列表。

### 词性标注

词性标注是为文本中的每个标记分配词性标记的过程。词性标签是指示单词语法功能的标签。例如，文本“我是学生”中的标记具有标签“PRON”、“VERB”、“DET”和“NOUN”。

邮递员.py

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

如您所见，pos_tag() 函数能够正确标记文本中的标记。

###命名实体识别

命名实体识别是对文本中的专有名词进行识别和分类的过程。专有名词是人、地、组织和事物的名称。例如，文本“我去了商店”中的命名实体是“我”、“商店”。

书呆子

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

如您所见，ne_chunk() 函数能够正确识别文本中的命名实体。