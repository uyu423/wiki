---
title: 010：使用 TensorFlow.js 和 Node.js 的长短期记忆 (LSTM)
description: 
published: true
date: 2023-02-02T09:04:29.074Z
tags: 
editor: markdown
dateCreated: 2023-02-02T09:04:24.710Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [010: Long Short-Term Memory (LSTM) with TensorFlow.js and Node.js***English** document is available*](/en/Knowledge-base/TensorFlow-js/Learning/010-long-short-term-memory-lstm-with-tensorflow-js-and-node-js)
{.links-list}


# 使用 TensorFlow.js 和 Node.js 的长短期记忆 (LSTM)

在本文中，我们将学习使用 TensorFlow.js 和 Node.js 的长短期记忆 (LSTM) 网络。我们将介绍什么是 LSTM 网络、它们如何工作以及如何训练它们。到本文结束时，您应该对如何使用 LSTM 网络以及如何将它们应用于不同的问题有一个很好的理解。

## 什么是 LSTM 网络？

LSTM 网络是一种循环神经网络 (RNN)。 RNN 是可以处理时序数据（例如时间序列数据或文本）的神经网络。 LSTM 网络是一种特殊类型的 RNN，可以学习长期依赖关系。这意味着他们可以长时间记住信息，这对于预测和分类等任务很有用。

## LSTM 网络是如何工作的？

LSTM 网络由 LSTM 单元组成。每个 LSTM 单元都有一个单元状态和一个输入门、一个输出门和一个遗忘门。细胞状态就像一个存储器，可以长时间存储信息。输入门控制当前输入的多少信息存储在细胞状态中。输出门控制从细胞状态输出多少信息。遗忘门控制遗忘先前细胞状态的信息量。

![LSTM 细胞](https://raw.githubusercontent.com/tensorflow/tfjs-layers/master/resources/lstm_cell.png)

LSTM 网络使用这些门来控制网络中的信息流。这使他们能够学习长期依赖关系。

## 如何训练 LSTM 网络？

可以使用多种方法训练 LSTM 网络。最常见的方法是使用时间反向传播 (BPTT)。 BPTT 是一种训练 RNN 的方法，其中梯度随时间向后传播。这允许网络从长数据序列中学习。

## 结论

在这篇文章中，我们了解了长短期记忆网络。我们讨论了它们是什么、它们如何工作以及如何培训它们。 LSTM 网络是从顺序数据中学习的强大工具。