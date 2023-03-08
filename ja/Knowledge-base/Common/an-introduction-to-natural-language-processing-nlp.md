---
title: 自然言語処理 (NLP) の紹介
description: 
published: true
date: 2023-01-31T05:57:45.617Z
tags: 
editor: markdown
dateCreated: 2023-01-31T05:57:43.968Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [An Introduction to Natural Language Processing (NLP)***English** version of this document is available*](/en/Knowledge-base/Common/an-introduction-to-natural-language-processing-nlp)
{.links-list}


#自然言語処理（NLP）の紹介

NLPは、人間とコンピュータの間の相互作用に関連するコンピュータサイエンスと人工知能の分野です。テキストを分析して意味を理解するのに役立ちます。

NLP は、次のようなさまざまなアプリケーションで使用されます。

- 感情分析
- 言語翻訳
- 音声認識
- チャットボット
- テキスト分類


## NLPとは？

NLPは人間の言語を理解し、それから意味を抽出する人工知能の1つの分野です。自分の言語で人間と対話できるコンピュータシステムを構築するために使用されます。

NLPは複雑な分野であり、さまざまな問題を解決するために使用できるさまざまな技術があります。この記事では、最も一般的なNLPの作業と技術について簡単に紹介します。

## NLP操作

###感情分析

感情分析は、テキストの感情的なトーンを決定するタスクです。ブランドや製品に関する世論を測定するためによく使用されます。

感情分析を実行する方法はいくつかありますが、一般的なアプローチの1つは、事前に訓練された機械学習モデルを使用することです。これらのモデルは、ラベル付きテキストの大規模なデータセットで学習され、新しいテキストの感情を予測するために使用できます。

以下の例では、TextBlobライブラリを使用して、いくつかの映画レビューの感情分析を実行します。 TextBlobはテキストデータの操作を容易にするPythonライブラリです。

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

#polarity = text.sentiment.polarity
#subjectivity = text.sentiment.subjectivity

text1 = "I loved the movie! It was so funny and exciting."
text2 = "I hated the movie. It was so boring and slow."

blob1 = TextBlob(text1)
blob2 = TextBlob(text2)

print(blob1.sentiment)
#(0.875、0.625)

print(blob2.sentiment)
#(-0.625、0.625)
```

ご覧のように、機械学習モデルは両方のテキストの感情を正しく分類できました。

###言語翻訳

言語翻訳は、テキストをある言語から別の言語に翻訳する作業です。多くの場合、さまざまな言語で同じことを言う方法がさまざまであるため、これはコンピュータにとって難しい作業です。

言語翻訳には、ルールベースの翻訳と機械翻訳の2つの一般的なアプローチがあります。

ルールベースの翻訳では、人間の言語学者は、ソース言語の単語とフレーズをターゲット言語にマッピングする一連のルールを作成します。このアプローチは非常に正確ですが、労働集約的で速度が遅くなる可能性があります。

機械翻訳は、機械学習アルゴリズムを使用してテキストを翻訳する方法を学ぶより自動化されたアプローチです。このアプローチははるかに高速ですが、時にはルールベースの翻訳よりも精度が低下する可能性があります。

次の例では、googletransライブラリのtranslate（）関数を使用してテキストを英語からスペイン語に翻訳します。 Google翻訳は、さまざまな言語間でテキストを翻訳できる機械翻訳サービスです。

```python
from googletrans import Translator

translator = Translator()

# The translate() function translates a text from one language to another.
# The src and dest parameters specify the source and target languages.
# The text parameter is the text to be translated.

result = translator.translate(text="Hello, world!", src="en", dest="es")

print(result.text)
#Hola、món！
```

ご覧のように、機械翻訳サービスはテキストを英語からスペイン語に正確に翻訳できます。

###音声認識

音声認識は、音声（音声信号）をテキストに変換する作業です。これは、同じことを言う方法がさまざまで、同じ人が毎回同じことを言うことができるので、コンピュータにとって難しい作業です。

音声認識には、ルールベースの音声認識と統計的音声認識という2つの一般的なアプローチがあります。

ルールベースの音声認識では、人間の言語学者は音を単語とフレーズにマッピングする一連のルールを作成します。このアプローチは非常に正確ですが、労働集約的で速度が遅くなる可能性があります。

統計的音声認識は、機械学習アルゴリズムを使用して音声認識方法を学習するより自動化されたアプローチです。このアプローチははるかに高速ですが、時にはルールベースの音声認識よりも精度が低下する可能性があります。

次の例では、SpeechRecognitionライブラリを使用してWAVオーディオファイル内の音声を認識しています。 SpeechRecognitionライブラリは、音声データの操作を容易にするPythonライブラリです。

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

#Hello、world！ 1.0
# This is a test. 0.8
```

ご覧のとおり、pocketsphinx音声認識エンジンはオーディオファイルから音声を正しく認識できました。

###チャットボット

チャットボットは、人間の言葉を理解し応答できるコンピュータプログラムです。彼らは通常、カスタマーサービスエージェントとして使用されます。

チャットボットは通常、機械学習アルゴリズムを使用して構築されます。最初のステップは、例会話のデータセットを作成することです。その後、このデータセットは機械学習モデルをトレーニングするために使用されます。次に、このモデルを使用して新しい入力に対する応答を生成します。

以下の例では、ChatterBotライブラリを使用してチャットボットを構築します。 ChatterBotはチャットボットを簡単に作成できるPythonライブラリです。

```python
from chatterbot import ChatBot

# The ChatBot class creates a new chatbot.

# The statement_comparison_function parameter is a function that is used
# to compare the similarity of two statements.
# The response_selection_method parameter is a function that is used to
# select a response from a list of responses.

bot = ChatBot(
    「ジョン」、
    statement_comparison_function=lambda a, b: a.confidence < b.confidence,
    response_selection_method=lambda a: a[0],
)

# The train() method trains the chatbot on a dataset of example conversations.
# The dataset is a list of tuples, where each tuple contains the input
# statement and the output response.

dataset = [
    ("Hello, world!", "Hello, John!")、
    ("How are you?", "I'm good, thanks for asking."),
    ("What is your favorite food?", "I like pizza!"),
]

bot.train(dataset)

# The get_response() method generates a response to an input statement.
# The input statement is specified as a string.

response = bot.get_response("Hello, world!")

print(response)
#Hello、ジョン！
```

ご覧のとおり、チャットボットは入力された文に正しく応答できました。

## NLP技術

自然言語処理に使用できるさまざまな技術があります。このセクションでは、最も一般的な技術のいくつかを紹介します。

###トークン化

トークン化は、テキストを個々のトークンに分割するプロセスです。トークンはテキストの基本的な意味単位です。たとえば、「I am a student」テキストのトークンは、「I」、「am」、「a」、および「student」です。

tokenize.py

```python
from nltk.tokenize import word_tokenize

# The word_tokenize() function from the NLTK library tokenizes a text
# into a list of words.

text = "I am a student"
tokens = word_tokenize(text)

print(tokens)
#['I', 'am', 'a', 'student']
```

ご覧のとおり、word_tokenize（）関数はテキストを単語リストに正しくトークン化できました。

###品詞タグ付け

品詞タグ付けは、テキストの各トークンに品詞タグを割り当てるプロセスです。品詞タグは、単語の文法的機能を表すラベルです。たとえば、「I am a student」テキストのトークンには、「PRON」、「VERB」、「DET」、および「NOUN」タグがあります。

postag.py

```python
from nltk import pos_tag

# The pos_tag() function from the NLTK library assigns a part of speech
# tag to each token in a text.

text = "I am a student"
tokens = word_tokenize(text)
tags = pos_tag(tokens)

print(tags)
#[('I', 'PRP'), ('am', 'VBP'), ('a', 'DT'), ('student', 'NN')]
```

ご覧のとおり、 pos_tag() 関数はテキストのトークンに正しくタグを付けることができました。

### オブジェクト名認識

名前付きエンティティ認識は、テキスト内の一意名詞を識別して分類するプロセスです。固有名詞は、人、場所、組織、物事の名前です。たとえば、「私は店に行きました」というテキストの名前付きエンティティは「私」、「ストア」です。

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
#[('I', 'PRP'), ('went', 'VBD'), ('to', 'TO'), ('the', 'DT'),
#('store', 'NN')]
```

ご覧のとおり、ne_chunk（）関数はテキスト内の名前付きエンティティを正しく識別できました。