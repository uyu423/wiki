---
title: 软件开发 010：Ruby on Rails
description: 
published: true
date: 2023-02-07T20:56:08.641Z
tags: 
editor: markdown
dateCreated: 2023-02-07T20:56:06.910Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Software Development 010: Ruby on Rails***English** document is available*](/en/Knowledge-base/Software-Development/Learning/software-development-010-ruby-on-rails)
{.links-list}


# 软件开发 010：Ruby on Rails

在本文中，我们将全面而实用地了解 Ruby on Rails——一种使用 Ruby 编程语言编写的流行 Web 开发框架。

我们将涵盖以下主题：

* 什么是 Ruby on Rails？
* 轨道MVC
* 安装 Ruby on Rails
* Rails目录结构
* 铁路路线
* 导轨控制器
* 轨道模型
* 轨道视图
* 轨道助手
* 轨道布局
* Rails 资产
* Rails 邮递员
* 轨道活动记录
* 轨道动作包
* 轨道动作视图
* Rails 动作邮件
* 轨道主动支持
* Rails 资产管道

## 什么是 Ruby on Rails？

Ruby on Rails 是一个用 Ruby 编程语言编写的 Web 开发框架。它旨在通过提供构建和部署 Web 应用程序的标准方法，使开发 Web 应用程序变得更容易和更快。

Rails 通常与 Ruby on Rails 框架一起使用，它提供了一组工具和库，可以更轻松地开发 Web 应用程序。

## 轨道 MVC

Ruby on Rails 基于模型视图控制器 (MVC) 架构模式。这是 Web 应用程序的常见设计模式，有助于保持代码的组织性和易于维护。

MVC模式由三部分组成：

* **模型**负责存储和检索数据。
* **View** 负责向用户显示数据。
* **Controller** 负责处理用户输入和交互。

## 在 Rails 上安装 Ruby

在您开始使用 Ruby on Rails 进行开发之前，您需要将它安装到您的计算机上。

有几种不同的方法可以安装 Ruby on Rails，但我们将使用 RubyInstaller 包。

1. 从[RubyInstaller网站](https://rubyinstaller.org/)下载RubyInstaller包。

2. 运行安装程序并按照提示进行操作。请务必选择“将 Ruby 可执行文件添加到您的 PATH”选项。

3. 安装完成后，打开一个新的终端窗口并键入 `ruby -v` 以验证 Ruby 是否已安装。你应该看到这样的东西：

```
ruby 2.6.3p62 (2019-04-16 revision 67580) [x86_64-darwin18]
```

4. 现在我们需要安装 Rails。为此，我们将使用 `gem` 命令，它是 Ruby 的包管理器。在终端中，键入“gem install rails”。这将安装最新版本的 Rails。

5. 要验证 Rails 是否已安装，请键入 `rails -v`。你应该看到这样的东西：

```
Rails 5.2.3
```

## Rails 目录结构

现在我们已经安装了 Ruby on Rails，让我们看一下 Rails 应用程序的目录结构。

Rails 应用程序由许多不同的文件夹和文件组成，每个文件夹和文件都有特定的用途。

以下是最重要的文件夹和文件的列表：

* `app` 文件夹包含您的应用程序的代码。
* `bin` 文件夹包含您的应用程序的可执行文件。
* `config` 文件夹包含您的应用程序的配置文件。
* `db` 文件夹包含您的应用程序的数据库文件。
* `lib` 文件夹包含您的应用程序的库文件。
* `log` 文件夹包含您的应用程序的日志文件。
* `public` 文件夹包含您的应用程序的静态文件。
* `test` 文件夹包含您的应用程序的测试文件。
* `tmp` 文件夹包含您的应用程序的临时文件。
* `vendor` 文件夹包含您的应用程序的第三方代码。

## 铁路路线

Rails 路由用于将 URL 映射到控制器操作。它们在 `config/routes.rb` 文件中定义。

例如，以下路由会将 URL `/articles` 映射到 `articles# index` 操作：

```ruby
get '/articles', to: 'articles#index'
```

Rails 还支持通配符路由，可用于将 URL 映射到带参数的控制器操作。

例如，以下路由会将 URL `/articles/:id` 映射到 `articles# show` 操作：

```ruby
get '/articles/:id', to: 'articles#show'
```

## 导轨控制器

Rails 控制器负责处理用户输入和交互。它们在 `app/controllers` 文件夹中定义。

每个控制器由许多动作组成，这些动作是负责处理特定请求的方法。

例如，`articles` 控制器可能有一个 `index` 操作来处理对 `/articles` URL 的请求，还有一个 `show` 操作来处理对 `/articles/:id` URL 的请求。

## 轨道模型

Rails 模型负责存储和检索数据。它们在 `app/models` 文件夹中定义。

每个模型代表一种特定的数据类型，例如“文章”或“用户”。模型通常用于在数据库中存储数据，但它们也可以用于存储其他格式的数据，例如 XML 或 JSON。

模型还可用于执行数据验证，例如确保“文章”具有标题和正文。

## Rails 视图

Rails 视图负责向用户显示数据。它们在 `app/views` 文件夹中定义。

视图通常以 HTML 编写，但也可以以其他格式编写，例如 XML 或 JSON。

视图也可以使用模板来 DRY up 他们的代码。例如，显示文章列表的视图可能使用负责显示单篇文章的模板。

## Rails 助手

Rails 助手是提供用于视图的实用方法的模块。它们在 `app/helpers` 文件夹中定义。

助手可用于格式化数据以供显示，例如将日期转换为人类可读的格式。它们还可用于生成 HTML 标记，例如链接或表单字段。

## 轨道布局

Rails 布局用于通过为所有视图定义通用布局来 DRY up 视图代码。它们在 `app/views/layouts` 文件夹中定义。

布局通常用 HTML 编写，但也可以用其他格式编写，例如 XML 或 JSON。

布局也可以使用模板来干燥他们的代码。例如，为所有视图定义通用页眉和页脚的布局可能使用负责显示视图内容的模板。

## Rails 资产

Rails 资产是应用程序使用的静态文件，例如图像、JavaScript 文件或 CSS 文件。它们存储在 `app/assets` 文件夹中。

Rails 还提供了资产管道，这是一组可用于处理和压缩资产的工具。

## Rails 邮件程序

Rails 邮件程序用于从您的应用程序发送电子邮件。它们在 `app/mailers` 文件夹中定义。

邮件程序可用于向用户发送通知，例如密码重置说明或新文章通知。

## Rails ActiveRecord

Rails ActiveRecord 是一个对象关系映射 (ORM) 库，用于与数据库交互。它在 `activerecord` gem 中定义。

ActiveRecord 提供了许多方法，可以更轻松地使用数据库，例如用于检索数据的“find”和用于存储数据的“save”。

## Rails 动作包

Rails ActionPack 是一组用于构建 Web 应用程序的库。它在 `actionpack` gem 中定义。

ActionPack 提供了许多方法和类，可以更轻松地开发 Web 应用程序，例如用于访问请求参数的“params”和用于呈现视图的“render”。

## Rails 动作视图

Rails ActionView 是一个用于呈现视图的库。它在 `actionview` gem 中定义。

ActionView 提供了很多方法和类，可以更方便地渲染视图，比如 render 渲染视图，partial 渲染局部视图。

## Rails ActionMailer

Rails ActionMailer 是一个用于从您的应用程序发送电子邮件的库。它在 `actionmailer` gem 中定义。

ActionMailer 提供了一些方法和类，可以更方便地发送电子邮件，例如 `mail` 发送电子邮件，以及 `attachments` 为电子邮件添加附件。

## Rails ActiveSupport

Rails ActiveSupport 是一组由 Rails 使用的实用程序类和模块。它在 `activesupport` gem 中定义。

ActiveSupport 提供了许多方法和类，可以更轻松地使用 Ruby 对象，例如用于复数和单数化单词的“Inflector”，以及用于格式化日期和时间的“Time”。

## Rails 资产管道

Rails 资产管道是一组可用于处理和压缩资产的工具。它在 `sprockets` gem 中定义。

Asset pipeline 提供了许多方法和类，可以更轻松地使用 assets，例如用于压缩 JavaScript 文件的 uglifier 和编译 Sass 文件的 sass 等。

## 结论

在本文中，我们全面而实用地了解了 Ruby on Rails。我们已经介绍了很多内容，但关于这个流行的 Web 开发框架还有更多需要了解的地方。

如果您想了解有关 Ruby on Rails 的更多信息，请查看以下资源：

* [Ruby on Rails 指南](https://guides.rubyonrails.org/)
* [Ruby on Rails API 文档](https://api.rubyonrails.org/)
* [Ruby on Rails 教程](https://www.railstutorial.org/)