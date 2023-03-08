---
title: 软件开发 030：自然语言处理 (NLP)
description: 
published: true
date: 2023-02-09T15:56:24.281Z
tags: 
editor: markdown
dateCreated: 2023-02-09T15:56:22.589Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Software Development 030: Natural Language Processing (NLP)***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-030-natural-language-processing-nlp)
{.links-list}


# 软件开发 030：自然语言处理 (NLP)

在这篇文章中，我们将全面而实用地了解自然语言处理 (NLP)。我们将介绍什么是 NLP、它的一些用途以及如何开始使用 Python 进行编码。

## 什么是自然语言处理？

自然语言处理 (NLP) 是计算机科学和人工智能的一个领域，涉及计算机与人类（自然）语言之间的交互，特别是如何对计算机进行编程以处理和分析大量自然语言数据。

NLP 用于构建聊天机器人、自动语音识别和机器翻译等应用程序。

## 自然语言处理任务

NLP 可以执行许多不同的任务。一些最常见的任务是：

- **文本分类：**为一段文本分配类别或标签，例如垃圾邮件检测、情绪分析。

- **信息提取：**从非结构化文本中提取结构化数据，例如从文档中提取日期、名称和位置。

- **自然语言生成：**从数据中生成文本，例如生成文档的摘要。

- **语音识别：**将语音转换为文本，例如语音到文本的应用程序。

- **机器翻译：**将文本从一种语言翻译成另一种语言，例如谷歌翻译。

## 自然语言处理入门

在本节中，我们将介绍使用 Python 进行 NLP 编码的基础知识。我们将使用自然语言工具包 (NLTK)，这是一个流行的 Python 库，用于处理人类语言数据。

### 安装 NLTK

在开始编码之前，我们需要安装 NLTK。 NLTK 可以使用 pip 安装，pip 是 Python 的包管理器：

```
pip install nltk
```

### 下载 NLTK 数据

安装 NLTK 后，我们需要下载 NLTK 将使用的数据。这些数据包括英语单词列表、语法规则等。

我们可以使用 NLTK 下载器下载这些数据：

```python
import nltk

nltk.download()
```

这将打开一个窗口，我们可以在其中选择要下载的数据。现在，我们只下载“流行”数据。

### NLTK 基础知识

现在我们已经安装了 NLTK 并下载了数据，我们可以开始使用 NLTK 的一些功能了。

首先，让我们导入 NLTK 库：

```python
import nltk
```

接下来，让我们选择要处理的文本。 NLTK 附带了许多我们可以使用的文本。对于这个例子，我们将使用“gutenberg”语料库，其中包含许多经典书籍：

```python
from nltk.corpus import gutenberg
```

现在我们已经加载了 gutenberg 语料库，我们可以访问它包含的文本。例如，要获取“爱丽丝梦游仙境”的文本，我们可以执行以下操作：

```python
alice = gutenberg.raw('carroll-alice.txt')
```

我们还可以访问文本中的单词：

```python
alice_words = gutenberg.words('carroll-alice.txt')
```

和句子：

```python
alice_sents = gutenberg.sents('carroll-alice.txt')
```

### 文本预处理

在我们对文本进行任何进一步分析之前，我们需要对其进行预处理。此预处理步骤包括以下内容：

- 标记化：将文本拆分为单独的单词或句子。

- 规范化：将单词转换为小写并删除标点符号。

- 词干提取或词形还原：将单词还原为其基本形式。

我们不会在这里详细介绍这些步骤中的每一个，但是 NLTK 提供了许多函数，可以轻松执行这些预处理步骤。

例如，要将文本标记为句子，我们可以使用 ```sent_tokenize``` 函数：

```python
from nltk.tokenize import sent_tokenize

sentences = sent_tokenize(alice)
```

要将文本标记为单词，我们可以使用 ```word_tokenize``` 函数：

```python
from nltk.tokenize import word_tokenize

words = word_tokenize(alice)
```

我们还可以通过将文本转换为小写并删除标点符号来规范化文本：

```python
from nltk.tokenize import RegexpTokenizer

tokenizer = RegexpTokenizer(r'\w+')

words = tokenizer.tokenize(alice.lower())
```

最后，我们可以对文本进行词干化或词形还原。词干提取将单词简化为其基本形式，例如“跑”变成“跑”。词形还原将单词简化为其基本形式，但会考虑单词的上下文，例如“跑”变成“跑”，“跑”变成“跑”。

```python
from nltk.stem import PorterStemmer, WordNetLemmatizer

stemmer = PorterStemmer()
lemmatizer = WordNetLemmatizer()

stemmed_words = [stemmer.stem(w) for w in words]
lemmatized_words = [lemmatizer.lemmatize(w) for w in words]
```

### 词性标注

词性 (POS) 标记是为文本中的每个单词分配 POS 标签的过程。词性标签是指示单词语法功能的标签，例如一个词是否是名词、动词、形容词等。

NLTK 提供了许多不同的词性标注器，但对于这个例子，我们将使用默认的词性标注器：

```python
from nltk import pos_tag

tagged_words = pos_tag(words)
```python
positive_words = ['good', 'great', 'awesome', 'fantastic', 'excellent']
negative_words = ['bad', 'terrible', 'horrible', 'awful', 'poor']
```python
from nltk import ne_chunk

named_entities = ne_chunk(tagged_words)
```蟒蛇
从 nltk 导入 ne_chunk

named_entities = ne_chunk(tagged_words)
```

```ne_chunk``` 函数的输出是一棵树，其中树中的每个节点代表一个命名实体。

### 文本分类

文本分类是为一段文本分配类别或标签的任务。例如，我们可能想将一段文本分类为“正面”或“负面”。

有许多不同的方法来处理文本分类，但对于这个例子，我们将使用一个简单的词袋方法。

首先，我们将创建一个正面和负面词的列表：

```python
num_positive_words = 0
num_negative_words = 0

for word in words:
    if word in positive_words:
        num_positive_words += 1
    elif word in negative_words:
        num_negative_words += 1
```

接下来，我们将计算文本中正面和负面单词的数量：

```python
if num_positive_words > num_negative_words:
    print('The text is positive.')
elif num_positive_words < num_negative_words:
    print('The text is negative.')
else:
    print('The text is neutral.')
```

最后，我们将根据正面和负面词的数量将文本分类为正面或负面：

```蟒蛇
如果 num_positive_words > num_negative_words：
    print('文字是正面的。')
elif num_positive_words < num_negative_words:
    print('文本是否定的。')
别的：
    print('文本是中性的。')
```

当然，这是一种非常简单的文本分类方法，在实践中，我们会使用更复杂的方法。

## 进一步阅读的资源

- [Natural Language Processing with Python](http://www.nltk.org/book/) - Python 中 NLP 的综合实用指南。

- [用于 NLP 的 Python：标记化、词干提取和词形还原](https://www.datacamp.com/community/tutorials/stemming-lemmatization-python) - 关于如何在 Python 中执行文本预处理的教程。

- [使用 NLTK 进行命名实体识别](https://towardsdatascience.com/named-entity-recognition-with-nltk-d0a87a1544f1) - 关于如何使用 NLTK 在 Python 中执行 NER 的教程。

- [使用 NLTK 进行文本分类](https://towardsdatascience.com/text-classification-with-nltk-d0a87a1544f1) - 关于如何使用 NLTK 在 Python 中执行文本分类的教程。