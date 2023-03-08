---
title: 061：将 Nest.js 与文件系统 API 结合使用
description: 
published: true
date: 2023-02-10T10:56:24.848Z
tags: 
editor: markdown
dateCreated: 2023-02-10T10:56:18.454Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [061: Using Nest.js with the Filesystem API***English** document is available*](/en/Knowledge-base/Nest-js/Learning/061-using-nest-js-with-the-filesystem-api)
{.links-list}


# 将 Nest.js 与文件系统 API 结合使用

Nest.js 是一个 Node.js 框架，可帮助您创建可扩展的服务器端应用程序。它使用 TypeScript 并与 Node.js 生态系统很好地集成。

在这篇文章中，我们将看到如何将 Nest.js 与文件系统 API 一起使用。我们将使用以下模块：

- [fs](https://nodejs.org/api/fs.html)：Node.js 文件系统模块。
- [路径](https://nodejs.org/api/path.html)：Node.js 路径模块。
- [util](https://nodejs.org/api/util.html)：Node.js util 模块。

## 读写文件

我们要做的第一件事是学习如何读写文件。我们将从一个读取文件并将其内容打印到控制台的简单示例开始。

```javascript
const fs = require('fs');

fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) {
    throw err;
  }

  console.log(data);
});
```

在上面的代码中，我们使用了 `fs.readFile()` 方法来读取文件的内容。第一个参数是文件路径，第二个参数是编码。回调函数有两个参数：一个 err 对象和文件中的 data。

如果出现错误，将设置 err 对象。否则，`data` 参数将包含文件的内容。

我们还可以使用 fs.readFileSync() 方法来同步读取文件。但是这种方法会阻塞事件循环，所以一般不推荐使用。

现在让我们看看如何写入文件。以下示例将字符串写入文件：

```javascript
const fs = require('fs');

fs.writeFile('file.txt', 'Hello, world!', 'utf8', (err) => {
  if (err) {
    throw err;
  }
});
```

在上面的代码中，我们使用了 `fs.writeFile()` 方法将字符串写入文件。第一个参数是文件路径，第二个参数是要写入的字符串，第三个参数是编码。回调函数接受一个参数：一个 err 对象。

如果出现错误，将设置 err 对象。否则文件写入成功。

我们也可以使用`fs.writeFileSync()` 方法来同步写入文件。但是这种方法会阻塞事件循环，所以一般不推荐使用。

## 追加文件

 有时我们需要将数据附加到现有文件而不是覆盖它。我们可以使用 `fs.appendFile()` 方法来做到这一点：

```javascript
const fs = require('fs');

fs.appendFile('file.txt', 'Hello, world!', 'utf8', (err) => {
  if (err) {
    throw err;
  }
});
```

在上面的代码中，我们使用了 `fs.appendFile()` 方法将字符串追加到文件中。第一个参数是文件的路径，第二个参数是要附加的字符串，第三个参数是编码。回调函数接受一个参数：一个 err 对象。

如果出现错误，将设置 err 对象。否则文件写入成功。

我们还可以使用 fs.appendFileSync() 方法同步追加文件。但是这种方法会阻塞事件循环，所以一般不推荐使用。

## 重命名文件

我们可以使用 `fs.rename()` 方法重命名文件：

```javascript
const fs = require('fs');

fs.rename('old-file.txt', 'new-file.txt', (err) => {
  if (err) {
    throw err;
  }
});
```

在上面的代码中，我们使用了 `fs.rename()` 方法来重命名文件。第一个参数是旧路径，第二个参数是新路径。回调函数接受一个参数：一个 err 对象。

如果出现错误，将设置 err 对象。否则，该文件将成功重命名。

我们还可以使用 fs.renameSync() 方法同步重命名文件。但是这种方法会阻塞事件循环，所以一般不推荐使用。

## 删除文件

我们可以使用 fs.unlink() 方法来删除文件：

```javascript
const fs = require('fs');

fs.unlink('file.txt', (err) => {
  if (err) {
    throw err;
  }
});
```

在上面的代码中，我们使用了 `fs.unlink()` 方法来删除文件。第一个参数是文件的路径。回调函数接受一个参数：一个 err 对象。

如果出现错误，将设置 err 对象。否则文件删除成功。

我们也可以使用 fs.unlinkSync() 方法同步删除文件。但是这种方法会阻塞事件循环，所以一般不推荐使用。

## 说明文件

我们可以使用 `fs.stat()` 方法来获取有关文件的信息：

```javascript
const fs = require('fs');

fs.stat('file.txt', (err, stats) => {
  if (err) {
    throw err;
  }

  console.log(stats);
});
```

在上面的代码中，我们使用了 `fs.stat()` 方法来获取有关文件的信息。第一个参数是文件的路径。回调函数有两个参数：一个 err 对象和一个 stats 对象。

如果出现错误，将设置 err 对象。否则，`stats` 对象将包含有关该文件的信息。

我们还可以使用 fs.statSync() 方法来同步获取有关文件的信息。但是这种方法会阻塞事件循环，所以一般不推荐使用。

## 看文件

我们可以使用 `fs.watch()` 方法来监视文件的变化：

```javascript
const fs = require('fs');

fs.watch('file.txt', (eventType, filename) => {
  console.log(eventType, filename);
});
```

在上面的代码中，我们使用了 `fs.watch()` 方法来监视文件的更改。第一个参数是文件的路径。回调函数有两个参数：一个“eventType”字符串和一个“filename”字符串。

`eventType` 参数将是以下之一：

- `rename`：文件已重命名。
- `change`：文件已更改。

如果文件被重命名，则 filename 参数将是文件的新路径，如果文件已更改，则为 null 。

我们还可以使用 fs.watchFile() 方法来监视文件的更改。但是，此方法使用轮询，这可能很昂贵。

## 阅读目录

我们可以使用 `fs.readdir()` 方法来读取目录的内容：

```javascript
const fs = require('fs');

fs.readdir('/path/to/directory', (err, files) => {
  if (err) {
    throw err;
  }

  console.log(files);
});
```

在上面的代码中，我们使用了 `fs.readdir()` 方法来读取目录的内容。第一个参数是目录的路径。回调函数有两个参数：一个 err 对象和一个 files 数组。

如果出现错误，将设置 err 对象。否则，`files` 数组将包含目录中文件的名称。

我们还可以使用 fs.readdirSync() 方法来同步读取目录的内容。但是这种方法会阻塞事件循环，所以一般不推荐使用。

## 创建目录

我们可以使用 `fs.mkdir()` 方法来创建一个目录：

```javascript
const fs = require('fs');

fs.mkdir('/path/to/directory', (err) => {
  if (err) {
    throw err;
  }
});
```

在上面的代码中，我们使用了 `fs.mkdir()` 方法来创建一个目录。第一个参数是目录的路径。回调函数接受一个参数：一个 err 对象。

如果出现错误，将设置 err 对象。否则目录创建成功。

我们也可以使用 fs.mkdirSync() 方法来同步创建目录。但是这种方法会阻塞事件循环，所以一般不推荐使用。

## 删除目录

我们可以使用 `fs.rmdir()` 方法来删除一个目录：

```javascript
const fs = require('fs');

fs.rmdir('/path/to/directory', (err) => {
  if (err) {
    throw err;
  }
});
```

在上面的代码中，我们使用了 `fs.rmdir()` 方法来删除一个目录。第一个参数是目录的路径。回调函数接受一个参数：一个 err 对象。

如果出现错误，将设置 err 对象。否则目录删除成功。

我们还可以使用 fs.rmdirSync() 方法来同步删除目录。但是这种方法会阻塞事件循环，所以一般不推荐使用。

## 结论

在本文中，我们了解了如何将 Nest.js 与文件系统 API 结合使用。我们已经学习了如何读写文件、如何向文件追加数据、如何重命名和删除文件、如何获取文件信息、如何监视文件的更改、如何读取目录的内容、如何创建和删除目录。