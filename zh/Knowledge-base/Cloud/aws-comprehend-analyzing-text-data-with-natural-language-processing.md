---
title: AWS Comprehend：使用自然语言处理分析文本数据
description: 
published: true
date: 2023-02-14T21:17:26.018Z
tags: 
editor: markdown
dateCreated: 2023-02-14T21:17:18.355Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [AWS Comprehend: Analyzing Text Data with Natural Language Processing***English** document is available*](/en/Knowledge-base/Cloud/aws-comprehend-analyzing-text-data-with-natural-language-processing)
{.links-list}



# AWS Comprehend：使用自然语言处理分析文本数据

文本数据无处不在。它存在于我们阅读的书籍、我们消费的新闻、我们分享的社交媒体帖子以及我们在做出购买决定时所依赖的客户评论中。这些数据可能非常有价值，但前提是我们能够从中提取意义。

自然语言处理 (NLP) 是计算机科学和人工智能的一个领域，处理计算机与人类（自然）语言之间的交互。 NLP 用于构建可以自动解释文本数据并从中提取含义的应用程序。

AWS Comprehend 是一种完全托管的 NLP 服务，可以轻松地从文本数据中提取含义。在本文中，我们将了解如何使用 AWS Comprehend 分析文本数据。

## 开始使用 AWS Comprehend

在开始使用 AWS Comprehend 之前，我们需要设置一个 AWS 账户并创建一个具有访问该服务权限的 IAM 用户。

拥有 AWS 账户后，您可以使用以下策略创建 IAM 用户：

```{language} {code}
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "comprehend:*"
            ],
            "Resource": "*"
        }
    ]
}
```

有了 IAM 用户，我们现在可以创建 AWS Comprehend 资源。为此，我们需要登录 AWS 管理控制台并导航到 AWS Comprehend 服务。

进入 AWS Comprehend 控制台后，我们可以创建一个新资源。我们需要为资源提供名称，选择区域，然后选择我们之前创建的 IAM 角色。

创建资源后，我们现在可以开始使用 AWS Comprehend。

## 分析文本数据

AWS Comprehend 为我们提供了许多不同的方法来分析文本数据。在本节中，我们将了解一些最常用的功能。

### 情绪分析

情感分析是一种从一段文本中自动提取情感（正面、负面或中性）的方法。这对于各种应用程序都非常有用，例如确定客户评论的整体情绪或了解社交媒体帖子的情绪。

要使用 AWS Comprehend 执行情绪分析，我们需要提供我们想要分析的文本。我们可以通过直接输入文本或提供文本所在的 URL 来做到这一点。

在我们提供文本后，AWS Comprehend 将对其进行分析并向我们提供文本的情感。

### 关键短语提取

关键短语提取是一种自动识别一段文本中的关键短语的方法。这对于各种应用程序都非常有用，例如识别客户评论的主题或理解社交媒体帖子的主题。

要使用 AWS Comprehend 执行关键短语提取，我们需要提供要分析的文本。我们可以通过直接输入文本或提供文本所在的 URL 来做到这一点。

在我们提供文本后，AWS Comprehend 将对其进行分析并向我们提供它提取的关键短语。

### 语言检测

语言检测是一种自动识别一段文本的语言的方法。这对于各种应用程序都非常有用，例如识别客户评论的语言或理解社交媒体帖子的语言。

要使用 AWS Comprehend 执行语言检测，我们需要提供要分析的文本。我们可以通过直接输入文本或提供文本所在的 URL 来做到这一点。

在我们提供文本后，AWS Comprehend 将对其进行分析并向我们提供它检测到的语言。

## 结论

在本文中，我们了解了如何使用 AWS Comprehend 分析文本数据。我们已经了解了如何使用 AWS Comprehend 执行情绪分析、关键短语提取和语言检测。

虽然我们只触及了 AWS Comprehend 的皮毛，但这应该足以让您入门。