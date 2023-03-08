---
title: 软件开发 075：负载测试
description: 
published: true
date: 2023-02-04T20:17:29.574Z
tags: 
editor: markdown
dateCreated: 2023-02-04T20:17:24.208Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Software Development 075: Load Testing***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-075-load-testing)
{.links-list}


## 介绍

负载测试是对系统或应用程序提出需求并测量其响应的过程。目标是确定系统或应用程序在各种负载条件下的行为方式。

负载测试很重要，因为它可以帮助识别系统或应用程序中潜在的性能瓶颈。它还可以帮助确定系统或应用程序可以处理的最大用户数量。

有许多不同的工具可用于负载测试。在这篇文章中，我们将重点介绍 Apache JMeter，它是一种流行的开源工具。

## 安装 Apache JMeter

Apache JMeter 可以从以下链接下载：

http://jmeter.apache.org/

下载文件后，将其解压缩，您应该会看到以下目录结构：

```
apache-jmeter-3.1
├── bin
├── docs
├── lib
└── printable_docs
```

## 创建测试计划

测试计划是 JMeter 将用来运行测试的一组指令。测试计划应包括以下要素：

- 线程组：这是 JMeter 将用来运行测试的一组线程。
- Sampler：这是 JMeter 将用来向系统或应用程序发送请求的元素。
- Listener：这是 JMeter 将用来收集和显示测试结果的元素。

要创建测试计划，请启动 JMeter，您应该会看到以下屏幕：

![JMeter 开始屏幕](https://i.imgur.com/VkzMv9w.png)

要添加线程组，请右键单击测试计划并选择添加 > 线程（用户）> 线程组。

![JMeter 线程组](https://i.imgur.com/DYUi4T4.png)

要添加采样器，请右键单击线程组并选择添加 > 采样器 > HTTP 请求。

![JMeter 采样器](https://i.imgur.com/iLKVLCy.png)

要添加监听器，请右键单击线程组并选择添加 > 监听器 > 查看结果树。

![JMeter 监听器](https://i.imgur.com/qoWql3Y.png)

## 配置测试计划

将线程组、采样器和侦听器添加到测试计划后，您需要配置它们。

要配置线程组，请选择它，您应该会看到以下选项：

![JMeter 线程组选项](https://i.imgur.com/g4vO4jQ.png)

- 线程数（用户）：这是 JMeter 将用于运行测试的线程数。
- 循环计数：这是 JMeter 将运行测试的次数。
- Ramp-Up Period（以秒为单位）：这是 JMeter 增加线程数所需的时间。

要配置采样器，请选择它，您应该会看到以下选项：

![JMeter 采样器选项](https://i.imgur.com/A1mlvkx.png)

- 协议：这是 JMeter 将用于发送请求的协议。
- 服务器名称或 IP：这是 JMeter 将向其发送请求的服务器名称或 IP 地址。
- 端口号：这是 JMeter 将用于发送请求的端口号。
- 路径：这是 JMeter 将用于发送请求的路径。

要配置侦听器，请选择它，您应该会看到以下选项：

![JMeter 侦听器选项](https://i.imgur.com/OcTGiuk.png)

- 输出文件：这是 JMeter 将用来输出测试结果的文件。
- 格式：这是输出结果的格式。

## 运行测试

配置测试计划后，您就可以运行测试了。要运行测试，请选择测试计划并单击运行按钮。

![JMeter 运行测试](https://i.imgur.com/L1G5fvk.png)

JMeter 现在将运行测试，您应该会在监听器中看到结果。

![JMeter 测试结果](https://i.imgur.com/Y6UgR8W.png)

## 分析结果

可以分析测试结果以确定系统或应用程序的性能。

以下指标可用于分析结果：

- 吞吐量：这是系统或应用程序每秒可以处理的请求数。
- 平均响应时间：这是系统或应用程序响应请求所花费的平均时间。
- 百分位数：这是需要一定时间才能响应的请求的百分比。

## 附加信息

- 重要的是要注意负载测试不应用于查找系统或应用程序中的错误。
- 负载测试可用于模拟不同类型的用户行为。
- JMeter 可用于测试 Web 应用程序和 Web 服务。

## 参考

- 阿帕奇 JMeter：https://jmeter.apache.org/
- JMeter 教程：https://www.tutorialspoint.com/jmeter/jmeter_tutorial.pdf
- JMeter 用户手册：https://jmeter.apache.org/usermanual/index.html