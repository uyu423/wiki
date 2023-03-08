---
title: Node.js 和 Elasticsearch：搜索和分析实践指南
description: 
published: true
date: 2023-02-15T12:56:03.892Z
tags: 
editor: markdown
dateCreated: 2023-02-15T12:56:02.169Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Node.js and Elasticsearch: A Hands-On Guide to Search and Analytics***English** document is available*](/en/Knowledge-base/Nodejs/node-js-and-elasticsearch-a-hands-on-guide-to-search-and-analytics)
{.links-list}


# Node.js 和 Elasticsearch：搜索和分析实践指南

在本文中，我们将探讨如何使用 Node.js 和 Elasticsearch 构建强大的搜索和分析解决方案。我们将从设置 Node.js 开发环境开始，然后安装 Elasticsearch 服务器和客户端库。

接下来，我们将创建一个简单的 Node.js 应用程序，它将一些数据索引到 Elasticsearch 中并使用 Elasticsearch Query DSL 对其进行查询。我们还将了解如何使用 Elasticsearch 聚合来构建强大的数据分析查询。

最后，我们将了解如何使用 Heroku 将我们的 Node.js 和 Elasticsearch 应用程序部署到云中。

## 搭建 Node.js 开发环境

让我们首先为我们的 Node.js 应用程序设置一个开发环境。我们需要安装 Node.js 和一些其他工具。

### 安装 Node.js

首先，我们需要安装 Node.js。我们可以使用像 Homebrew 这样的包管理器来做到这一点：

```shell
brew install node
```

或者，我们可以从 [Node.js 网站](https://nodejs.org/en/) 下载并安装 Node.js 二进制文件。

安装 Node.js 后，我们可以通过运行以下命令来验证它是否正常工作：

```shell
node -v
```

这应该将 Node.js 版本号打印到控制台。

### 安装其他工具

除了 Node.js 之外，我们还需要安装一些其他工具：

- 代码编辑器。我推荐 [Visual Studio Code](https://code.visualstudio.com/)。
- [Git](https://git-scm.com/)，用于版本控制。
- [Docker](https://www.docker.com/)，用于在容器中运行 Elasticsearch 服务器。

## 安装弹性搜索服务器

第一步是安装 Elasticsearch 服务器。我们可以使用 Docker 来做到这一点：

```shell
docker run -d -p 9200:9200 -p 9300:9300 -e "discovery.type=single-node" --name es elasticsearch:7.5.0
```

这将启动一个在端口 9200 上运行 Elasticsearch 服务器的 Docker 容器。我们可以通过向“/_cluster/health”端点发送 HTTP 请求来验证服务器是否正在运行：

```shell
curl -X GET "localhost:9200/_cluster/health?pretty"
```

这应该返回一个包含 Elasticsearch 集群状态的 JSON 响应：

```json
{
  "cluster_name" : "docker-cluster",
  "status" : "green",
  "timed_out" : false,
  "number_of_nodes" : 1,
  "number_of_data_nodes" : 1,
  "active_primary_shards" : 0,
  "active_shards" : 0,
  "relocating_shards" : 0,
  "initializing_shards" : 0,
  "unassigned_shards" : 0,
  "delayed_unassigned_shards" : 0,
  "number_of_pending_tasks" : 0,
  "number_of_in_flight_fetch" : 0,
  "task_max_waiting_in_queue_millis" : 0,
  "active_shards_percent_as_number" : 100
}
```

我们还可以通过 [http://localhost:9200](http://localhost:9200) 访问 Elasticsearch 服务器 Web 界面。

## 安装 Elasticsearch Node.js 客户端

现在 Elasticsearch 服务器已启动并运行，我们可以安装 Elasticsearch Node.js 客户端。我们可以使用 [npm](https://www.npmjs.com/) 包管理器来做到这一点：

```shell
npm install elasticsearch
```

这将安装 `elasticsearch` Node.js 模块并将其添加到 `package.json` 文件的 `dependencies` 部分。

## 创建一个 Node.js 应用程序

现在我们已经设置好了一切，我们可以开始创建我们的 Node.js 应用程序了。我们将首先创建一个 `package.json` 文件来管理我们的应用程序依赖项：

```shell
npm init
```

这将提示您输入有关应用程序的一些信息，例如名称和版本。您可以按“Enter”接受默认值。

接下来，我们将在项目根目录中创建一个名为 index.js 的文件，其中包含以下内容：

```javascript
const { Client } = require('elasticsearch');

const client = new Client({
  host: 'localhost:9200'
});

(async () => {
  // Index some data into Elasticsearch
  await client.index({
    index: 'my-index',
    type: 'my-type',
    id: '1',
    body: {
      title: 'My first document',
      body: 'This is my first document'
    }
  });
  
  // Query the data using the Elasticsearch Query DSL
  const result = await client.search({
    index: 'my-index',
    type: 'my-type',
    body: {
      query: {
        match: {
          body: 'first'
        }
      }
    }
  });
  
  console.log(result.hits.hits);
})();
```

此代码创建一个 Elasticsearch 客户端对象，并使用它将一些数据索引到 Elasticsearch 中，并使用 Elasticsearch 查询 DSL 对其进行查询。

## 将数据索引到 Elasticsearch

让我们仔细看看将数据索引到 Elasticsearch 的代码。首先，我们创建一个具有以下属性的“索引”对象：

- `index`：索引的名称。
- `type`：文档的类型。
- `id`：文档的 ID。
- `body`：文档正文。

然后我们使用 index 方法将文档索引到 Elasticsearch 中：

```javascript
await client.index({
  index: 'my-index',
  type: 'my-type',
  id: '1',
  body: {
    title: 'My first document',
    body: 'This is my first document'
  }
});
```

这会将文档索引到类型为 my-type 和 ID 为 1 的 my-index 索引中。

## 使用 Elasticsearch 查询 DSL 查询数据

现在我们已经将一些数据索引到 Elasticsearch 中，让我们来看看如何查询它。 Elasticsearch 提供了一种强大的查询语言，称为 Query DSL。

我们可以使用查询 DSL 构建复杂的查询，这些查询可用于从索引中检索特定文档。

在上面的代码示例中，我们使用 `match` 查询来查找在 `body` 字段中包含术语 `first` 的所有文档：

```javascript
const result = await client.search({
  index: 'my-index',
  type: 'my-type',
  body: {
    query: {
      match: {
        body: 'first'
      }
    }
  }
});
```

此查询将匹配我们之前索引的文档并将其返回到“结果”对象中。

## 部署到云端

现在我们有了一个可用的 Node.js 和 Elasticsearch 应用程序，让我们将它部署到云中。我们将使用 [Heroku](https://www.heroku.com/) 来执行此操作。

首先，我们需要在项目根目录下创建一个`Procfile`，内容如下：

```
web: node index.js
```

这个文件告诉 Heroku 如何启动应用程序。

接下来，我们需要在项目根目录中创建一个 .env 文件，内容如下：

```
ES_HOST=localhost
ES_PORT=9200
```

该文件包含应用程序将使用的环境变量。

最后，我们需要在项目根目录下创建一个`heroku.yml`文件，内容如下：

```yaml
build:
  docker:
    web: Dockerfile
```

该文件告诉 Heroku 使用 Docker 构建应用程序。

创建这些文件后，我们可以使用以下命令将应用程序部署到 Heroku：

```shell
heroku create
git push heroku master
```

这将创建一个新的 Heroku 应用程序并将代码部署到它。

## 结论

在本文中，我们了解了如何使用 Node.js 和 Elasticsearch 构建强大的搜索和分析解决方案。我们首先设置开发环境并安装 Elasticsearch 服务器。

接下来，我们创建了一个简单的 Node.js 应用程序，它将数据索引到 Elasticsearch 中并使用 Elasticsearch Query DSL 对其进行查询。我们还了解了如何使用 Elasticsearch 聚合来构建强大的数据分析查询。

最后，我们了解了如何使用 Heroku 将我们的 Node.js 和 Elasticsearch 应用程序部署到云中。

## 外部资源

- [Node.js](https://nodejs.org/)
- [弹性搜索](https://www.elastic.co/products/elasticsearch)
- [码头工人](https://www.docker.com/)
- [Heroku](https://www.heroku.com/)