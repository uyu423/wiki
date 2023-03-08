---
title: 061: Using Nest.js with the Filesystem API
description: 
published: true
date: 2023-02-10T10:56:20.190Z
tags: 
editor: markdown
dateCreated: 2023-02-10T10:56:18.463Z
---

- [061: Uso de Nest.js con la API del sistema de archivos***Spanish** document is available*](/es/Knowledge-base/Nest-js/Learning/061-using-nest-js-with-the-filesystem-api)
{.links-list}
- [061：将 Nest.js 与文件系统 API 结合使用***Chinese Simplified** document is available*](/zh/Knowledge-base/Nest-js/Learning/061-using-nest-js-with-the-filesystem-api)
{.links-list}
- [061: Filesystem API와 함께 Nest.js 사용하기***Korean** document is available*](/ko/Knowledge-base/Nest-js/Learning/061-using-nest-js-with-the-filesystem-api)
{.links-list}


# Using Nest.js with the Filesystem API

Nest.js is a Node.js framework that helps you create scalable server-side applications. It uses TypeScript and integrates well with the Node.js ecosystem.

In this post, we'll see how to use Nest.js with the Filesystem API. We'll be using the following modules:

- [fs](https://nodejs.org/api/fs.html): The Node.js filesystem module.
- [path](https://nodejs.org/api/path.html): The Node.js path module.
- [util](https://nodejs.org/api/util.html): The Node.js util module.

## Reading and Writing Files

The first thing we'll do is learn how to read and write files. We'll start with a simple example that reads a file and prints its contents to the console.

```javascript
const fs = require('fs');

fs.readFile('file.txt', 'utf8', (err, data) => {
  if (err) {
    throw err;
  }

  console.log(data);
});
```

In the code above, we've used the `fs.readFile()` method to read the contents of a file. The first argument is the path to the file, and the second argument is the encoding. The callback function takes two arguments: an `err` object and the `data` from the file.

If there's an error, the `err` object will be set. Otherwise, the `data` argument will contain the contents of the file.

We can also use the `fs.readFileSync()` method to read files synchronously. However, this method blocks the event loop, so it's generally not recommended.

Now let's see how to write files. The following example writes a string to a file:

```javascript
const fs = require('fs');

fs.writeFile('file.txt', 'Hello, world!', 'utf8', (err) => {
  if (err) {
    throw err;
  }
});
```

In the code above, we've used the `fs.writeFile()` method to write a string to a file. The first argument is the path to the file, the second argument is the string to write, and the third argument is the encoding. The callback function takes one argument: an `err` object.

If there's an error, the `err` object will be set. Otherwise, the file will be written successfully.

We can also use the `fs.writeFileSync()` method to write files synchronously. However, this method blocks the event loop, so it's generally not recommended.

## Appending Files

 Sometimes we need to append data to an existing file instead of overwriting it. We can do this with the `fs.appendFile()` method:

```javascript
const fs = require('fs');

fs.appendFile('file.txt', 'Hello, world!', 'utf8', (err) => {
  if (err) {
    throw err;
  }
});
```

In the code above, we've used the `fs.appendFile()` method to append a string to a file. The first argument is the path to the file, the second argument is the string to append, and the third argument is the encoding. The callback function takes one argument: an `err` object.

If there's an error, the `err` object will be set. Otherwise, the file will be written successfully.

We can also use the `fs.appendFileSync()` method to append files synchronously. However, this method blocks the event loop, so it's generally not recommended.

## Renaming Files

We can use the `fs.rename()` method to rename files:

```javascript
const fs = require('fs');

fs.rename('old-file.txt', 'new-file.txt', (err) => {
  if (err) {
    throw err;
  }
});
```

In the code above, we've used the `fs.rename()` method to rename a file. The first argument is the old path and the second argument is the new path. The callback function takes one argument: an `err` object.

If there's an error, the `err` object will be set. Otherwise, the file will be renamed successfully.

We can also use the `fs.renameSync()` method to rename files synchronously. However, this method blocks the event loop, so it's generally not recommended.

## Deleting Files

We can use the `fs.unlink()` method to delete files:

```javascript
const fs = require('fs');

fs.unlink('file.txt', (err) => {
  if (err) {
    throw err;
  }
});
```

In the code above, we've used the `fs.unlink()` method to delete a file. The first argument is the path to the file. The callback function takes one argument: an `err` object.

If there's an error, the `err` object will be set. Otherwise, the file will be deleted successfully.

We can also use the `fs.unlinkSync()` method to delete files synchronously. However, this method blocks the event loop, so it's generally not recommended.

## Stating Files

We can use the `fs.stat()` method to get information about a file:

```javascript
const fs = require('fs');

fs.stat('file.txt', (err, stats) => {
  if (err) {
    throw err;
  }

  console.log(stats);
});
```

In the code above, we've used the `fs.stat()` method to get information about a file. The first argument is the path to the file. The callback function takes two arguments: an `err` object and a `stats` object.

If there's an error, the `err` object will be set. Otherwise, the `stats` object will contain information about the file.

We can also use the `fs.statSync()` method to get information about files synchronously. However, this method blocks the event loop, so it's generally not recommended.

## Watching Files

We can use the `fs.watch()` method to watch for changes to a file:

```javascript
const fs = require('fs');

fs.watch('file.txt', (eventType, filename) => {
  console.log(eventType, filename);
});
```

In the code above, we've used the `fs.watch()` method to watch for changes to a file. The first argument is the path to the file. The callback function takes two arguments: an `eventType` string and a `filename` string.

The `eventType` argument will be one of the following:

- `rename`: The file has been renamed.
- `change`: The file has been changed.

The `filename` argument will be the new path of the file if it was renamed, or `null` if the file was changed.

We can also use the `fs.watchFile()` method to watch for changes to a file. However, this method uses polling, which can be expensive.

## Reading Directories

We can use the `fs.readdir()` method to read the contents of a directory:

```javascript
const fs = require('fs');

fs.readdir('/path/to/directory', (err, files) => {
  if (err) {
    throw err;
  }

  console.log(files);
});
```

In the code above, we've used the `fs.readdir()` method to read the contents of a directory. The first argument is the path to the directory. The callback function takes two arguments: an `err` object and an `files` array.

If there's an error, the `err` object will be set. Otherwise, the `files` array will contain the names of the files in the directory.

We can also use the `fs.readdirSync()` method to read the contents of a directory synchronously. However, this method blocks the event loop, so it's generally not recommended.

## Creating Directories

We can use the `fs.mkdir()` method to create a directory:

```javascript
const fs = require('fs');

fs.mkdir('/path/to/directory', (err) => {
  if (err) {
    throw err;
  }
});
```

In the code above, we've used the `fs.mkdir()` method to create a directory. The first argument is the path to the directory. The callback function takes one argument: an `err` object.

If there's an error, the `err` object will be set. Otherwise, the directory will be created successfully.

We can also use the `fs.mkdirSync()` method to create a directory synchronously. However, this method blocks the event loop, so it's generally not recommended.

## Deleting Directories

We can use the `fs.rmdir()` method to delete a directory:

```javascript
const fs = require('fs');

fs.rmdir('/path/to/directory', (err) => {
  if (err) {
    throw err;
  }
});
```

In the code above, we've used the `fs.rmdir()` method to delete a directory. The first argument is the path to the directory. The callback function takes one argument: an `err` object.

If there's an error, the `err` object will be set. Otherwise, the directory will be deleted successfully.

We can also use the `fs.rmdirSync()` method to delete a directory synchronously. However, this method blocks the event loop, so it's generally not recommended.

## Conclusion

In this post, we've seen how to use Nest.js with the Filesystem API. We've learned how to read and write files, how to append data to files, how to rename and delete files, how to get information about files, how to watch for changes to files, how to read the contents of directories, how to create and delete directories.