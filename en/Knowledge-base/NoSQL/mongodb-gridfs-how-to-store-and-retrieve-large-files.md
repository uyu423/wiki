---
title: MongoDB GridFS: How to Store and Retrieve Large Files
description: 
published: true
date: 2023-03-12T14:33:27.935Z
tags: 
editor: markdown
dateCreated: 2023-03-12T14:33:27.935Z
---

- [MongoDB GridFS: 대용량 파일 저장 및 검색 방법***Korean** document is available*](/ko/Knowledge-base/NoSQL/mongodb-gridfs-how-to-store-and-retrieve-large-files)
{.links-list}

MongoDB GridFS: How to Store and Retrieve Large Files

MongoDB is a popular NoSQL database that offers scalability, high performance, and flexibility to store and manage data of various types. It is widely used in modern web development to handle large volumes of data, including files. However, MongoDB has a default document size limit of 16MB, which can be a limitation when you need to store and retrieve large files, such as images, videos, or documents. That's where MongoDB GridFS comes in. In this article, we'll explore what MongoDB GridFS is, how it works, and how to use it to store and retrieve large files.

## What is MongoDB GridFS?

MongoDB GridFS is a specification for storing and retrieving large files in MongoDB. It uses two collections to store files: `fs.files` and `fs.chunks`. The `fs.files` collection stores metadata about the files, such as filename, content type, size, and upload date. The `fs.chunks` collection stores the binary data of the files in 255KB chunks. The files are split into chunks automatically by MongoDB when they are larger than the chunk size, and each chunk is stored as a separate document in the `fs.chunks` collection, with a reference to the `fs.files` document that represents the file.

GridFS is not a separate database or storage system but a way to use MongoDB as a file system for storing and retrieving large files. It provides a unified API for storing, retrieving, and deleting files, which makes it easy to integrate with MongoDB applications. GridFS supports multiple programming languages and platforms, including Node.js, Java, Python, and .NET.

## How does MongoDB GridFS work?

When you store a file using GridFS, MongoDB automatically splits the file into chunks and stores them in the `fs.chunks` collection. The metadata of the file is stored in the `fs.files` collection as a document with the following fields:

- `_id`: a unique identifier for the file
- `filename`: the name of the file
- `contentType`: the MIME type of the file (e.g. `image/jpeg`)
- `length`: the size of the file in bytes
- `chunkSize`: the size of the chunks in which the file is stored (default is 255KB)
- `uploadDate`: the date and time when the file was uploaded
- `md5`: the MD5 hash of the file's contents

The `fs.chunks` collection stores the binary data of the file in one or more chunk documents with the following fields:

- `_id`: a unique identifier for the chunk
- `files_id`: the `_id` value of the corresponding document in the `fs.files` collection
- `n`: the sequence number of the chunk within the file
- `data`: the binary data of the chunk

When you retrieve a file using GridFS, MongoDB retrieves the metadata document from the `fs.files` collection and the chunk documents from the `fs.chunks` collection and combines them to reconstruct the original file.

## How to use MongoDB GridFS

To use MongoDB GridFS, you need to install the MongoDB driver for your programming language or platform. Here, we'll use the Node.js driver as an example.

### Storing a file using GridFS

To store a file using GridFS in Node.js, you can use the `GridFSBucket` class provided by the MongoDB Node.js driver. Here's an example of storing a file:

```javascript
const { MongoClient } = require('mongodb');
const { GridFSBucket } = require('mongodb');

const uri = 'mongodb://localhost:27017/mydb';
const client = new MongoClient(uri);
await client.connect();

const db = client.db('mydb');
const bucket = new GridFSBucket(db);

const stream = bucket.openUploadStream('myFile.txt');
fs.createReadStream('/path/to/myFile.txt').pipe(stream);
```

In this example, we first connect to the MongoDB server using the `MongoClient` class. Then, we open a connection to the `mydb` database and create a `GridFSBucket` instance for it. We use the `openUploadStream()` method of the `GridFSBucket` instance to create an upload stream for the file `myFile.txt`. We then pipe the file contents from a readable stream (`fs.createReadStream('/path/to/myFile.txt')`) to the upload stream. MongoDB automatically splits the file into chunks and stores them in the `fs.chunks` collection, and the metadata of the file is stored in the `fs.files` collection.

### Retrieving a file using GridFS

To retrieve a file using GridFS in Node.js, you can use the `GridFSBucket` class provided by the MongoDB Node.js driver. Here's an example of retrieving a file:

```javascript
const { MongoClient } = require('mongodb');
const { GridFSBucket } = require('mongodb');

const uri = 'mongodb://localhost:27017/mydb';
const client = new MongoClient(uri);
await client.connect();

const db = client.db('mydb');
const bucket = new GridFSBucket(db);

const downloadStream = bucket.openDownloadStreamByName('myFile.txt');
downloadStream.pipe(fs.createWriteStream('/path/to/downloadedFile.txt'));
```

In this example, we first connect to the MongoDB server using the `MongoClient` class. Then, we open a connection to the `mydb` database and create a `GridFSBucket` instance for it. We use the `openDownloadStreamByName()` method of the `GridFSBucket` instance to create a download stream for the file `myFile.txt`. We then pipe the contents of the download stream to a writable stream (`fs.createWriteStream('/path/to/downloadedFile.txt')`) to save the file to disk.

### Deleting a file using GridFS

To delete a file using GridFS in Node.js, you can use the `GridFSBucket` class provided by the MongoDB Node.js driver. Here's an example of deleting a file:

```javascript
const { MongoClient } = require('mongodb');
const { GridFSBucket } = require('mongodb');

const uri = 'mongodb://localhost:27017/mydb';
const client = new MongoClient(uri);
await client.connect();

const db = client.db('mydb');
const bucket = new GridFSBucket(db);

bucket.delete('myFile.txt');
```

In this example, we first connect to the MongoDB server using the `MongoClient` class. Then, we open a connection to the `mydb` database and create a `GridFSBucket` instance for it. We use the `delete()` method of the `GridFSBucket` instance to delete the file `myFile.txt`. MongoDB automatically deletes the metadata document from the `fs.files` collection and the chunk documents from the `fs.chunks` collection.

## Conclusion

MongoDB GridFS is a powerful feature that allows you to store and retrieve large files in MongoDB. It provides a unified API for handling files and supports multiple programming languages and platforms. With GridFS, you can use MongoDB as a file system for your applications, which simplifies the management of large volumes of data. In this article, we've covered the basics of GridFS, how it works, and how to use it to store, retrieve, and delete files using Node.js. We hope this article has been useful and informative. 

## External Resources

- [MongoDB GridFS documentation](https://docs.mongodb.com/manual/core/gridfs/)
- [MongoDB Node.js driver documentation](https://mongodb.github.io/node-mongodb-native/)
- [Using GridFS to store and serve files in Node.js](https://www.twilio.com/blog/file-uploads-storing-retrieving-files-using-mongodb-gridfs-node-js)