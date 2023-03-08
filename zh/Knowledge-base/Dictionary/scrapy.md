---
title: Scrapy
description: 
published: true
date: 2023-02-14T20:55:58.140Z
tags: 
editor: markdown
dateCreated: 2023-02-14T20:55:55.721Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Scrapy***English** document is available*](/en/Knowledge-base/Dictionary/scrapy)
{.links-list}


# 概述
Scrapy 是一个用 Python 编写的免费开源网络爬虫框架。它用于从网站提取数据，可用于广泛的应用，例如数据挖掘、信息处理或历史档案。

# 描述
Scrapy 是一个网络爬虫框架，它提供了一个完整的工具包来从网站中提取数据。它被设计成快速、简单和可扩展的。该框架建立在 Twisted 异步网络库之上，并提供用于定义和运行网络蜘蛛的高级接口。

Scrapy 蜘蛛可以用 Python 编写，并使用简单的语法来定义要从网站中提取的数据。该框架提供了一组内置功能，例如支持从 HTML 和 XML 文档中选择和提取数据，以及支持跟踪链接和抓取多个页面。它还包括一个用于在云中运行蜘蛛的网络服务和一个用于监控和管理蜘蛛的网络控制台。

Scrapy 用于各种应用程序，例如数据挖掘、信息处理或历史存档。它可用于从网站中提取结构化数据，例如联系信息、产品列表或价格。它还用于自动化网络抓取任务，例如从多个页面收集数据或多次从单个页面抓取数据。

# 历史
Scrapy 于 2008 年由网络抓取和数据处理公司 Scrapinghub 首次发布。它是作为商业网络抓取工具的开源替代品创建的，并已成为最流行的网络抓取框架之一。

# 特征
Scrapy 提供了一系列功能，使网络抓取更容易、更高效：

- 支持从 HTML 和 XML 文档中选择和提取数据。
- 支持跟踪链接和抓取多个页面。
- 内置支持从 JavaScript 呈现的网站中提取数据。
- 用于在云中运行蜘蛛的 Web 服务。
- 用于监控和管理蜘蛛的 Web 控制台。
- 用于运行蜘蛛的命令行界面。
- 用于扩展框架的插件系统。

# 例子
下面是一个从网站中提取数据的 Scrapy 蜘蛛的例子：

```python
import scrapy

class MySpider(scrapy.Spider):
    name = "myspider"
    start_urls = ["http://example.com/"]
    
    def parse(self, response):
        for product in response.css('div.product'):
            yield {
                'name': product.css('h3.name::text').get(),
                'price': product.css('span.price::text').get(),
            }
```

# 优点和缺点
Scrapy 提供了一系列功能，使其成为网络抓取的强大工具。它快速、易于使用且可扩展。它还为从 JavaScript 呈现的网站中提取数据提供了内置支持。

然而，Scrapy 并不适合所有的网页抓取任务。它仅限于从网站提取数据，不支持其他类型的数据源，如数据库或 API。

# 相关技术
Scrapy 与其他网络抓取框架相关，例如 Beautiful Soup 和 Selenium。它还与 Apify 和 ParseHub 等网络抓取服务有关。

# 题外话
Scrapy 不仅用于网页抓取，还可以用于网页自动化任务，例如填写表格和提交数据。

# 其他的
Scrapy 是一个流行的开源网络抓取框架，用 Python 编写。它用于从网站中提取数据，可用于广泛的应用程序。它提供了一组使网络抓取更容易和更高效的功能，例如支持从 HTML 和 XML 文档中选择和提取数据，以及支持跟踪链接和抓取多个页面。