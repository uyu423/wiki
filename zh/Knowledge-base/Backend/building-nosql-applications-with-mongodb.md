---
title: 使用 MongoDB 构建 NoSQL 应用程序
description: 
published: true
date: 2023-02-01T22:06:04.229Z
tags: 
editor: markdown
dateCreated: 2023-02-01T22:06:01.502Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Building NoSQL Applications with MongoDB***English** document is available*](/en/Knowledge-base/Backend/building-nosql-applications-with-mongodb)
{.links-list}


# 使用 MongoDB 构建 NoSQL 应用程序

## 介绍

MongoDB是由10gen开发和支持的开源的面向文档的数据库系统。它是 NoSQL 数据库系统家族的一部分。 NoSQL 数据库越来越多地用于 Web 应用程序，因为它们可以处理高流量和数据量。

MongoDB 使用类似 JSON 的文档格式，并具有基于索引的搜索功能。它还具有丰富的查询语言。这些特性使 MongoDB 成为希望构建 NoSQL 应用程序的开发人员的一个有吸引力的选择。

## 设置 MongoDB

在本节中，我们将介绍设置 MongoDB 的基础知识。我们将在本地机器上安装 MongoDB 并创建一个简单的数据库。

### 安装 MongoDB

可以从 10gen 网站 (http://www.10gen.com/) 下载 MongoDB。有适用于 Windows、OS X 和 Linux 的版本。下载 MongoDB 后，按照适用于您的操作系统的说明进行安装。

### 创建数据库

我们将创建一个简单的数据库来存储有关书籍的信息。该数据库将有两个集合：一个用于书籍，一个用于作者。

首先，我们需要启动 MongoDB 服务器。对于 Windows，这可以通过运行“mongod”可执行文件来完成。对于 OS X 和 Linux，可以通过从终端运行“mongod”命令来启动 MongoDB。

MongoDB 服务器运行后，我们可以使用 `mongo` 客户端连接到它。这将为我们提供一个 `mongod>` 提示符，我们可以在其中输入命令。

首先，我们需要创建 books 集合。我们可以使用 `db.createCollection()` 方法来做到这一点：

    ```javascript
    db.createCollection("书籍")
    ```

然后我们可以使用 `db.books.insert()` 方法将一些数据插入到集合中。我们将为每本书插入一个文档：

    ```javascript
    db.books.insert({
        “标题”：“白鲸记”，
        “作者”：“赫尔曼梅尔维尔”，
        “年”：1851
    })

    db.books.insert({
        "title": "麦田里的守望者",
        “作者”：“J.D.塞林格”，
        “年”：1951
    })

    db.books.insert({
        "title": "杀死一只知更鸟",
        “作者”：“哈珀李”，
        “年”：1960
    })
    ```

然后我们可以创建 `authors` 集合并使用相同的方法将数据插入其中：

    ```javascript
    db.createCollection("作者")

    db.authors.insert({
        "name": "赫尔曼梅尔维尔",
        “出生”：1819年，
        “死于”：1891 年，
        “书籍”：[“白鲸记”]
    })

    db.authors.insert({
        "name": "J.D.塞林格",
        “出生”：1919年，
        “死”：2010年，
        “书籍”：[“麦田里的守望者”]
    })

    db.authors.insert({
        "姓名": "哈珀李",
        “出生”：1926年，
        “死”：2016年，
        “书籍”：[“杀死一只知更鸟”]
    })
    ```

然后我们可以使用 `db.collection.find()` 方法来查询集合中的数据。例如，要查找 J.D. Salinger 撰写的所有书籍，我们将使用以下查询：

    ```javascript
    db.books.find({"author": "J.D. Salinger"})
    ```

## 构建 NoSQL 应用程序

在本节中，我们将构建一个简单的 Web 应用程序来显示有关书籍的信息。我们将使用在上一节中创建的 MongoDB 数据库。

我们将使用 Node.js 平台构建应用程序。 Node.js 是用于构建 Web 应用程序的流行平台。它是轻量级的，并且有一个庞大的模块生态系统，可用于向应用程序添加功能。

我们将使用 Express.js Web 应用程序框架。 Express.js 是使用 Node.js 构建 Web 应用程序的流行选择。它易于使用并具有大量功能。

我们将使用 Jade 模板引擎为我们的网页生成 HTML。 Jade 是一种流行的模板引擎，易于使用并生成干净的 HTML。

我们将使用 Mongoose.js 模块来连接我们的 MongoDB 数据库。 Mongoose.js 是一个流行的模块，可以轻松地从 Node.js 使用 MongoDB。

### 安装依赖项

首先，我们需要安装我们将要使用的模块。我们可以使用 Node.js 中包含的 `npm` 包管理器来完成此操作。我们将全局安装模块，以便我们可以从命令行使用它们。

从命令行，我们可以使用以下命令安装我们需要的模块：

    npm 安装 -g 快递
    npm 安装-g 玉
    npm 安装 -g 猫鼬

### 创建应用程序

我们现在将为我们的应用程序创建文件。首先，我们将在应用程序的根目录中创建一个名为 app.js 的文件。该文件将包含我们的 Web 应用程序的代码。

我们将从要求我们安装的模块开始，并设置我们应用程序的基本结构：

    ```javascript
    var express = require("快递");
    var jade = require("玉");
    var mongoose = require("猫鼬");

    var app = express();

    app.set("视图引擎", "jade");
    app.set("views", __dirname + "/views");

    app.use(express.static(__dirname + "/public"));
    ```

然后我们将定义我们的路线。我们将创建两条路线：一条用于主页，一条用于图书详情页。

对于主页路由，我们将查询 books 集合并呈现一个显示结果的模板：

    ```javascript
    app.get("/", 函数(req, res) {
        db.books.find（函数（错误，书籍）{
            如果（错误）{
                // 处理错误
            } 别的 {
                res.render("index", { books: books });
            }
        });
    });
    ```

对于书籍详细信息页面，我们将查询 `books` 和 `authors` 集合并呈现一个显示结果的模板：

    ```javascript
    app.get("/book/:id", function(req, res) {
        db.books.findById(req.params.id, function(err, book) {
            如果（错误）{
                // 处理错误
            } 别的 {
                db.authors.findById(book.author, function(err, author) {
                    如果（错误）{
                        // 处理错误
                    } 别的 {
                        res.render("book", { book: book, author: 作者 });
                    }
                });
            }
        });
    });
    ```

然后我们将定义我们的模板。我们将创建两个模板：一个用于主页，一个用于图书详细信息页面。

对于主页模板，我们将遍历 `books` 数组并显示每本书的信息：

    ```玉
    扩展布局

    块内容
        h1=标题

        乌尔
            书中的每一本书
                李
                    a(href="/book/# {book._id}")= book.title
    ```

对于图书详情页面模板，我们将显示有关图书和作者的信息：

    ```玉
    扩展布局

    块内容
        h1= book.title

        p
            |撰写者
            a(href="/author/# {author._id}")= 作者姓名

        p = book.year
    ```

然后，我们将在 views 目录中创建一个名为 layout.jade 的文件。该文件将包含我们应用程序的布局模板：

    ```玉
    文档类型 html
    网页格式
        头
            标题=标题
            链接（rel='stylesheet', href='/stylesheets/style.css'）
        身体
            块内容
    ```

然后我们将在 `public/stylesheets` 目录中创建一个名为 `style.css` 的文件。该文件将包含我们应用程序的 CSS：

    ```CSS
    身体 {
        字体系列：无衬线；
    }

    h1 {
        字体粗细：正常；
    }
    ```

然后，我们将在应用程序的根目录中创建一个名为 `package.json` 的文件。该文件将包含我们应用程序的依赖项：

    ```javascript
    {
        “名称”：“图书应用程序”，
        “版本”：“0.0.1”，
        “依赖”：{
            “表达”：“3.x”，
            “玉”：“1.x”，
            “猫鼬”：“3.x”
        }
    }
    ```

然后，我们将在应用程序的根目录中创建一个名为“Procfile”的文件。该文件将告诉 Heroku 如何启动我们的应用程序：

    ```
    网络：节点 app.js
    ```

### 连接数据库

我们现在将修改我们的 app.js 文件以连接到我们的 MongoDB 数据库。我们将使用 `mongoose.connect()` 方法连接到数据库。我们将连接存储在一个名为 db 的变量中，以便我们可以在我们的路由中使用它：

    ```javascript
    var db = mongoose.connect("mongodb://localhost/book-app");
    ```

然后我们将定义我们的模型。我们将创建两种模型：一种用于书籍，一种用于作者。

对于书籍模型，我们将定义要存储在数据库中的字段：

    ```javascript
    var bookSchema = mongoose.Schema({
        标题：字符串，
        作者：mongoose.Schema.Types.ObjectId，
        年份：数字
    });

    var Book = mongoose.model("Book", bookSchema);
    ```

对于作者模型，我们将定义要存储在数据库中的字段：

    ```javascript
    var authorSchema = mongoose.Schema({
        名称：字符串，
        出生：数字，
        死亡：数字，
        书籍：[mongoose.Schema.Types.ObjectId]
    });

    var Author = mongoose.model("作者", authorSchema);
    ```

然后我们将修改我们的路线以使用我们的模型。

对于主页路由，我们将查询 books 集合并呈现一个显示结果的模板：

    ```javascript
    app.get("/", 函数(req, res) {
        Book.find（函数（错误，书籍）{
            如果（错误）{
                // 处理错误
            } 别的 {
                res.render("index", { books: books });
            }
        });
    });
    ```

对于书籍详细信息页面，我们将查询 `books` 和 `authors` 集合并呈现一个显示结果的模板：

    ```javascript
    app.get("/book/:id", function(req, res) {
        Book.findById(req.params.id, function(err, book) {
            如果（错误）{
                // 处理错误
            } 别的 {
                Author.findById(book.author, function(err, author) {
                    如果（错误）{
                        // 处理错误
                    } 别的 {
                        res.render("book", { book: book, author: 作者 });
                    }
                });
            }
        });
    });
    ```

## 部署应用程序

在本节中，我们会将应用程序部署到 Heroku。 Heroku 是一种流行的平台即服务 (PaaS)，可以轻松部署和扩展 Web 应用程序。

我们首先需要创建一个 Heroku 帐户 (https://signup.heroku.com/)。创建帐户后，您需要安装 Heroku Toolbelt (https://toolbelt.heroku.com/)。 Heroku Toolbelt 是一个命令行界面 (CLI)，可用于管理 Heroku 应用程序。

安装 Heroku Toolbelt 后，您可以使用“heroku login”命令登录您的帐户。系统将提示您输入电子邮件地址和密码。

然后我们可以使用 heroku create 命令创建我们的 Heroku 应用程序。这将创建一个新的应用程序并为其指定一个唯一的名称。我们可以选择使用 `--app` 标志为我们的应用程序指定一个名称：

    heroku create --app 我的应用程序名称

然后我们可以使用 `git push heroku master` 命令将我们的应用程序部署到 Heroku。这会将我们的代码从 Git 存储库的 `master` 分支推送到 `heroku` 远程：

    git push heroku 大师

然后我们可以使用 `heroku open` 命令在网络浏览器中打开我们的应用程序。这将在新选项卡中打开我们应用程序的主页：

    打开

## 结论

在本文中，我们介绍了使用 MongoDB 构建 NoSQL 应用程序的基础知识。我们已经介绍了如何安装 MongoDB、如何创建数据库、如何构建 NoSQL 应用程序以及如何将应用程序部署到 Heroku。

NoSQL 数据库在 Web 应用程序中越来越受欢迎。 MongoDB 因其面向文档的数据模型、基于索引的搜索功能和丰富的查询语言而成为 NoSQL 应用程序的热门选择。

Node.js 是用于构建 Web 应用程序的流行平台。它重量轻，拥有庞大的模块生态系统。 Express.js 是一个流行的 Node.js Web 应用程序框架。 Jade 是一种流行的模板引擎，易于使用并生成干净的 HTML。 Mongoose.js 是一个流行的模块，可以轻松地从 Node.js 使用 MongoDB。

Heroku 是一种流行的平台即服务 (PaaS)，可以轻松部署和扩展 Web 应用程序。