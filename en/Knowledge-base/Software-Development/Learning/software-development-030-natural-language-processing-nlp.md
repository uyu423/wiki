---
title: Software Development 030: Natural Language Processing (NLP)
description: 
published: true
date: 2023-02-09T15:56:28.796Z
tags: 
editor: markdown
dateCreated: 2023-02-09T15:56:22.593Z
---

- [Desarrollo de software 030: Procesamiento del lenguaje natural (PNL)***Spanish** document is available*](/es/Knowledge-base/Software-Development/Learning/software-development-030-natural-language-processing-nlp)
{.links-list}
- [软件开发 030：自然语言处理 (NLP)***Chinese Simplified** document is available*](/zh/Knowledge-base/Software-Development/Learning/software-development-030-natural-language-processing-nlp)
{.links-list}
- [소프트웨어 개발 030: 자연어 처리(NLP)***Korean** document is available*](/ko/Knowledge-base/Software-Development/Learning/software-development-030-natural-language-processing-nlp)
{.links-list}


# Software Development 030: Natural Language Processing (NLP)

In this post, we'll be taking a comprehensive and practical look at Natural Language Processing (NLP). We'll cover what NLP is, some of the tasks it's used for, and how to get started with coding in Python.

## What is NLP?

Natural Language Processing (NLP) is a field of computer science and artificial intelligence concerned with the interactions between computers and human (natural) languages, in particular how to program computers to process and analyze large amounts of natural language data.

NLP is used to build applications such as chatbots, automatic speech recognition, and machine translation.

## NLP Tasks

There are many different tasks that can be performed with NLP. Some of the most common tasks are:

- **Text classification:** Assigning a category or label to a piece of text, e.g. spam detection, sentiment analysis.

- **Information extraction:** Extracting structured data from unstructured text, e.g. extracting dates, names, and locations from a document.

- **Natural language generation:** Generating text from data, e.g. generating a summary of a document.

- **Speech recognition:** Converting speech to text, e.g. speech-to-text applications.

- **Machine translation:** Translating text from one language to another, e.g. Google Translate.

## Getting Started with NLP

In this section, we'll cover the basics of coding in Python for NLP. We'll be using the Natural Language Toolkit (NLTK), a popular Python library for working with human language data.

### Installing NLTK

Before we can start coding, we need to install NLTK. NLTK can be installed using pip, a package manager for Python:

```
pip install nltk
```

### downloading NLTK data

Once NLTK is installed, we need to download the data that NLTK will use. This data includes things like lists of English words, grammar rules, etc.

We can download this data using the NLTK downloader:

```python
import nltk

nltk.download()
```

This will open a window where we can select which data to download. For now, we'll just download the "popular" data.

### NLTK Basics

Now that we have NLTK installed and the data downloaded, we can start playing around with some of the features of NLTK.

First, let's import the NLTK library:

```python
import nltk
```

Next, let's choose a text to work with. NLTK comes with a number of texts that we can use. For this example, we'll use the "gutenberg" corpus, which contains a number of classic books:

```python
from nltk.corpus import gutenberg
```

Now that we have the gutenberg corpus loaded, we can access the texts that it contains. For example, to get the text of "Alice's Adventures in Wonderland" we can do the following:

```python
alice = gutenberg.raw('carroll-alice.txt')
```

We can also access the words in the text:

```python
alice_words = gutenberg.words('carroll-alice.txt')
```

And the sentences:

```python
alice_sents = gutenberg.sents('carroll-alice.txt')
```

### Text Pre-processing

Before we can do any further analysis of the text, we need to pre-process it. This pre-processing step includes things like:

- Tokenization: Splitting the text into individual words or sentences.

- Normalization: Converting the words to lowercase and removing punctuation.

- Stemming or lemmatization: reducing a word to its base form.

We won't go into too much detail on each of these steps here, but NLTK provides a number of functions that make it easy to perform these pre-processing steps.

For example, to tokenize a text into sentences, we can use the ```sent_tokenize``` function:

```python
from nltk.tokenize import sent_tokenize

sentences = sent_tokenize(alice)
```

To tokenize a text into words, we can use the ```word_tokenize``` function:

```python
from nltk.tokenize import word_tokenize

words = word_tokenize(alice)
```

We can also normalize the text by converting it to lowercase and removing punctuation:

```python
from nltk.tokenize import RegexpTokenizer

tokenizer = RegexpTokenizer(r'\w+')

words = tokenizer.tokenize(alice.lower())
```

Finally, we can stem or lemmatize the text. Stemming reduces a word to its base form, e.g. "running" becomes "run". Lemmatization reduces a word to its base form, but takes into account the context of the word, e.g. "running" becomes "run" but "ran" becomes "run".

```python
from nltk.stem import PorterStemmer, WordNetLemmatizer

stemmer = PorterStemmer()
lemmatizer = WordNetLemmatizer()

stemmed_words = [stemmer.stem(w) for w in words]
lemmatized_words = [lemmatizer.lemmatize(w) for w in words]
```

### Part-of-Speech Tagging

Part-of-speech (POS) tagging is the process of assigning a POS tag to each word in a text. POS tags are labels that indicate the grammatical function of a word, e.g. whether a word is a noun, verb, adjective, etc.

NLTK provides a number of different POS taggers, but for this example, we'll use the default POS tagger:

```python
from nltk import pos_tag

tagged_words = pos_tag(words)
```

The output of the ```pos_tag``` function is a list of tuples, where each tuple consists of a word and its POS tag.

### Named Entity Recognition

Named Entity Recognition (NER) is the task of identifying named entities in a text, e.g. people, places, organizations, etc.

NLTK provides a number of different NER taggers, but for this example, we'll use the default NER tagger:

```python
from nltk import ne_chunk

named_entities = ne_chunk(tagged_words)
```

The output of the ```ne_chunk``` function is a tree, where each node in the tree represents a named entity.

### Text Classification

Text classification is the task of assigning a category or label to a piece of text. For example, we might want to classify a piece of text as "positive" or "negative."

There are a number of different ways to approach text classification, but for this example, we'll use a simple bag-of-words approach.

First, we'll create a list of positive and negative words:

```python
positive_words = ['good', 'great', 'awesome', 'fantastic', 'excellent']
negative_words = ['bad', 'terrible', 'horrible', 'awful', 'poor']
```

Next, we'll count the number of positive and negative words in our text:

```python
num_positive_words = 0
num_negative_words = 0

for word in words:
    if word in positive_words:
        num_positive_words += 1
    elif word in negative_words:
        num_negative_words += 1
```

Finally, we'll classify the text as positive or negative based on the number of positive and negative words:

```python
if num_positive_words > num_negative_words:
    print('The text is positive.')
elif num_positive_words < num_negative_words:
    print('The text is negative.')
else:
    print('The text is neutral.')
```

Of course, this is a very simplistic approach to text classification and in practice, we would use more sophisticated methods.

## Resources for Further Reading

- [Natural Language Processing with Python](http://www.nltk.org/book/) - A comprehensive and practical guide to NLP in Python.

- [Python for NLP: Tokenization, Stemming, and Lemmatization](https://www.datacamp.com/community/tutorials/stemming-lemmatization-python) - A tutorial on how to perform text pre-processing in Python.

- [Named Entity Recognition with NLTK](https://towardsdatascience.com/named-entity-recognition-with-nltk-d0a87a1544f1) - A tutorial on how to perform NER in Python using NLTK.

- [Text Classification with NLTK](https://towardsdatascience.com/text-classification-with-nltk-d0a87a1544f1) - A tutorial on how to perform text classification in Python using NLTK.