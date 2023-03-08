---
title: Kotlin 和 Ruby on Rails：使用 Ruby 框架构建 Web 应用程序
description: 
published: true
date: 2023-01-31T08:15:36.117Z
tags: 
editor: markdown
dateCreated: 2023-01-31T08:15:33.417Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Kotlin and Ruby on Rails: Building a Web Application with a Ruby Framework***English** version of this document is available*](/en/Knowledge-base/Kotlin/kotlin-and-ruby-on-rails-building-a-web-application-with-a-ruby-framework)
{.links-list}
 提供的代码。

Kotlin 和 Ruby on Rails：使用 Ruby 框架构建 Web 应用程序

当您想要构建 Web 应用程序时，您有多种框架可供选择。 Ruby on Rails 是一种用于构建 Web 应用程序的流行框架，而 Kotlin 是一种因其与 Java 的互操作性及其安全特性而越来越受欢迎的语言。在本文中，我们将向您展示如何使用 Ruby on Rails 框架和 Kotlin 构建 Web 应用程序。

我们假设您熟悉 Kotlin 和 Ruby on Rails 的基础知识。如果您不了解，可以使用许多资源来了解有关这些技术的更多信息。

# # 设置 Kotlin/Ruby on Rails 项目

我们需要做的第一件事是建立一个 Kotlin/Ruby on Rails 项目。我们将使用以下工具：

* 科特林 1.3.72
* 红宝石 2.6.5
* 轨道 6.0.3.2

您可以使用彼此兼容的这些工具的任何版本。

要设置新的 Kotlin/Ruby on Rails 项目，我们将使用带有 -api 选项和 -d 选项的 rails new 命令来指定数据库。我们将使用 PostgreSQL 数据库。

    $ rails new my_app -api -d postgresql

这将创建一个名为 my_app 的新目录，其中包含一个基本的 Rails 应用程序。

# # 配置 Kotlin

接下来，我们需要将 Kotlin 添加到我们的项目中。我们将通过将 kotlin-rails 插件添加到我们项目的 Gemfile 来完成此操作。

    组：开发做
      宝石'kotlin-rails'
    结尾

然后，我们需要安装插件。

    $ 捆绑安装

现在我们已经安装了插件，我们需要配置 Kotlin。我们将通过在配置目录中创建一个名为 kotlin.yml 的文件来完成此操作。在这个文件中，我们将添加以下配置：

    科特林：
      版本：1.3.72
      目标：
        -jvm-1.8

这将告诉 Kotlin 使用版本 1.3.72 并编译为 Java 8 字节码。

# # 创建模型

现在我们已经设置了项目，可以开始构建我们的 Web 应用程序了。我们将从创建一些模型开始。在 Ruby on Rails 中，模型是表示我们应用程序中数据的类。我们将为应用程序中的每种类型的数据创建一个模型。

我们的第一个模型将是用户模型。我们将使用 rails generate 命令生成这个模型。

    $ rails 生成模型用户

这将创建一个名为 app/models/user.rb 的新文件。我们将打开此文件并添加以下代码：

    用户类 < ApplicationRecord
      有安全密码
    结尾

此代码定义了一个名为 User 的新模型。 has_secure_password 宏向我们的模型添加了一些方法来帮助我们安全地存储密码。

接下来，我们需要为我们的模型生成迁移。迁移是包含用于创建或修改数据库表的 SQL 代码的文件。要生成迁移，我们将再次使用 rails generate 命令。

    $ rails 生成迁移 create_users

这将在 db/migrate 目录中创建一个新文件。我们将打开此文件并添加以下代码：

    类 CreateUsers < ActiveRecord::Migration[6.0]
      定义更改
        create_table ：用户做|t|
          t.string :名称
          t.string：电子邮件
          t.string：密码摘要
          t.时间戳
        结尾
      结尾
    结尾

此代码创建一个名为 users 的新数据库表。该表包含名称、电子邮件和 password_digest 列。 password_digest 列是 has_secure_password 宏存储密码散列的地方。

现在我们已经创建了模型和迁移，我们需要运行迁移来创建数据库表。我们可以通过运行以下命令来完成此操作：

    $ 轨道数据库：迁移

# # 创建控制器

现在我们已经设置好模型，可以开始创建控制器了。在 Ruby on Rails 中，控制器是处理传入 HTTP 请求的类。我们将为要处理的每种类型的请求创建一个控制器。

我们的第一个控制器将是一个用于用户注册的控制器。我们将使用 rails generate 命令生成这个控制器。

    $ rails 生成控制器用户

这将创建一个名为 app/controllers/users_controller.rb 的新文件。我们将打开此文件并添加以下代码：

    类 UsersController < ApplicationController
      定义新
        @user = User.new
      结尾
    
      定义创建
        @user = User.new(user_params)
    
        如果@user.save
          会话 [:user_id] = @user.id
          重定向到根路径
        别的
          渲染：新
        结尾
      结尾
    
      私人的
    
      定义 user_params
        params.require(:user).permit(:name, :email, :password, :password_confirmation)
      结尾
    结尾

此代码定义了一个名为 UsersController 的新控制器。控制器有两个动作，新建和创建。新操作呈现用于创建新用户的表单。创建操作调用 User.create 方法来创建新用户。如果成功创建用户，则用户登录并重定向到主页。如果用户未成功创建，将再次呈现该表单并显示错误消息。

# # 创建视图

现在我们已经设置了模型和控制器，我们可以开始创建视图了。在 Ruby on Rails 中，视图是包含网页 HTML 代码的文件。我们将为应用程序中的每一页创建一个视图文件。

我们的第一个视图文件将是用户注册表单的文件。我们将在 app/views/users 目录中创建此文件。该文件将被称为 new.html.erb，它将包含以下代码：

    <%= form_for @user do |f| %>
      <%= f.label :name %>
      <%= f.text_field :name %>
    
      <%= f.label :email %>
      <%= f.text_field :email %>
    
      <%= f.label :密码 %>
      <%= f.password_field :密码 %>
    
      <%= f.label :password_confirmation %>
      <%= f.password_field :password_confirmation %>
    
      <%= f.submit %>
    <%结束%>

此代码创建用于创建新用户的表单。该表单包含姓名、电子邮件、密码和密码确认字段。表单被提交给 UsersController 的创建操作。

# # 配置路由

现在我们已经设置了我们的视图，我们需要配置我们的路由。路由是我们的应用程序响应的 URL。我们将在 config/routes.rb 文件中配置我们的路由。我们将打开此文件并添加以下代码：

    Rails.application.routes.draw 做
      资源：用户，仅：[：新，：创建]
    结尾

此代码定义了两条路线，一条用于新操作，一条用于 UsersController 的创建操作。

# # 测试应用程序

现在我们已经设置了应用程序，我们可以对其进行测试。我们将从启动 Rails 服务器开始。

    $ 轨道服务器

然后，我们将在网络浏览器中访问 http://localhost:3000。我们应该看到用户注册表。我们可以填写表格并提交。如果一切正常，我们应该会看到主页。

## 结论

在本文中，我们向您展示了如何使用 Ruby on Rails 框架和 Kotlin 构建 Web 应用程序。我们已经创建了模型、控制器和视图。我们还配置了路由并测试了我们的应用程序。