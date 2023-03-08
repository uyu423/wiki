---
title: 使用 TypeScript 和 Multer 处理文件上传和下载
description: 
published: true
date: 2023-02-17T18:15:42.599Z
tags: 
editor: markdown
dateCreated: 2023-01-30T23:36:52.576Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}
- [Handling File Uploads and Downloads with TypeScript and Multer***English** version of this document is available*](/en/Knowledge-base/TypeScript/handling-file-uploads-and-downloads-with-typescript-and-multer)
{.links-list}


# 使用 TypeScript 和 Multer 处理文件上传和下载

## 上传和下载文件是网络应用程序的常见任务。 Multer 是一个用于处理 multipart/form-data 的 Node.js 中间件，主要用于上传文件。 TypeScript 是 JavaScript 的超集，可为您的代码提供类型化特性。在本文中，我们将了解如何使用 TypeScript 和 Multer 上传文件。

我们将首先安装所需的依赖项。您可以使用以下命令安装 Multer：

```
npm install multer
```

可以使用以下命令安装 TypeScript：

```
npm install typescript
```

安装依赖项后，让我们创建一个 TypeScript 文件并将其命名为“index.ts”。我们将从初始化 Multer 的实例开始：

```typescript
import multer from "multer";

const upload = multer();
```

这里创建的 `upload` 对象将帮助我们处理文件上传过程。 `multer` 函数接受一个选项对象，可用于配置文件上传。例如，我们可以指定上传文件的目的地，如下所示：

```typescript
const upload = multer({dest: "uploads/"});
```

在这种情况下，文件将上传到 uploads 目录。我们还可以指定上传文件的名称：

```typescript
const upload = multer({
  dest: "uploads/",
  fileFilter: function(req, file, cb) {
    const ext = path.extname(file.originalname);
    if (ext !== ".jpg" && ext !== ".jpeg" && ext !== ".png") {
      return cb(new Error("Only jpg, jpeg, and png files are allowed"));
    }
    cb(null, true);
  },
  filename: function(req, file, cb) {
    cb(null, file.fieldname + "-" + Date.now());
  }
});
```

在上面的代码中，我们指定只允许使用 `jpg`、`jpeg` 和 `png` 文件。我们还指定上传文件的名称应为“fieldname-timestamp”，其中“fieldname”是表单字段的名称，“timestamp”是当前时间戳。

一旦配置了 upload 对象，我们就可以使用它来处理文件上传。例如，我们可以定义一个路由来处理文件上传，如下所示：

```typescript
app.post("/upload", upload.single("avatar"), (req, res) => {
  res.send("File uploaded successfully");
});
```

在上面的代码中，我们定义了一个到 `/upload` 的 `POST` 路由。 `upload.single()` 方法用于处理单个文件的上传。 `avatar` 字段用于指定包含该文件的表单字段的名称。 `req` 对象在 `req.file` 中包含上传的文件。在回调函数中，我们只是发送一个响应，说明文件已成功上传。

我们也可以使用 upload.array() 方法来处理多个文件的上传：

```typescript
app.post("/upload", upload.array("photos", 12), (req, res) => {
  res.send("Files uploaded successfully");
});
```

在上面的代码中，我们指定最多可以上传 12 个文件。 `photos` 字段用于指定包含文件的表单字段的名称。 `req.files` 数组包含上传的文件。

我们也可以使用 upload.fields() 方法来处理混合字段：

```typescript
app.post(
  "/upload",
  upload.fields([
    { name: "avatar", maxCount: 1 },
    { name: "photos", maxCount: 8 }
  ]),
  (req, res) => {
    res.send("Files uploaded successfully");
  }
);
```

在上面的代码中，我们定义了一个到 `/upload` 的 `POST` 路由。 `upload.fields()` 方法用于处理混合字段。我们已经指定要处理一个“avatar”字段和一个“photos”字段。 `avatar` 字段最多可以有 1 个文件，`photos` 字段最多可以有 8 个文件。

我们还可以使用 upload.none() 方法来处理不包含文件的字段：

```typescript
app.post("/profile", upload.none(), (req, res) => {
  // req.body contains the text fields
  res.send("Profile updated successfully");
});
```

在上面的代码中，我们定义了一个到 `/profile` 的 `POST` 路由。 `upload.none()` 方法用于处理不包含文件的字段。 `req.body` 对象包含文本字段。

我们还可以使用 upload.any() 方法来处理任何类型的字段：

```typescript
app.post("/contact", upload.any(), (req, res) => {
  // req.body contains the text fields and the files
  res.send("Message sent successfully");
});
```

在上面的代码中，我们定义了一个到 `/contact` 的 `POST` 路由。 `upload.any()` 方法用于处理任何类型的字段。 `req.body` 对象包含文本字段和文件。

## 下载文件是网络应用程序的另一个常见任务。我们可以使用 TypeScript 和 Multer 下载文件。例如，假设我们在 uploads 目录中有一个名为 avatar.jpg 的文件。我们可以定义一个路径来下载这个文件，如下所示：

```typescript
app.get("/download/:file(*)", (req, res) => {
  const file = req.params.file;
  const fileLocation = path.join(__dirname + "/uploads/", file);
  res.download(fileLocation, file);
});
```

在上面的代码中，我们定义了一个到 `/download/:file(*)` 的 `GET` 路由。 `:file` 参数表示要下载的文件的名称。 `__dirname` 变量包含当前目录的路径。 `fileLocation` 变量包含要下载的文件的路径。 `res.download()` 方法用于下载文件。

我们还可以使用 `res.sendFile()` 方法来发送文件：

```typescript
app.get("/download/:file(*)", (req, res) => {
  const file = req.params.file;
  const fileLocation = path.join(__dirname + "/uploads/", file);
  res.sendFile(fileLocation);
});
```

在上面的代码中，我们定义了一个到 `/download/:file(*)` 的 `GET` 路由。 `:file` 参数表示要下载的文件的名称。 `__dirname` 变量包含当前目录的路径。 `fileLocation` 变量包含要下载的文件的路径。 `res.sendFile()` 方法用于发送文件。

我们还可以使用 `res.attachment()` 方法将文件作为附件发送：

```typescript
app.get("/download/:file(*)", (req, res) => {
  const file = req.params.file;
  const fileLocation = path.join(__dirname + "/uploads/", file);
  res.attachment(fileLocation);
});
```

在上面的代码中，我们定义了一个到 `/download/:file(*)` 的 `GET` 路由。 `:file` 参数表示要下载的文件的名称。 `__dirname` 变量包含当前目录的路径。 `fileLocation` 变量包含要下载的文件的路径。 `res.attachment()` 方法用于将文件作为附件发送。

我们还可以使用 `res.redirect()` 方法将用户重定向到另一个页面：

```typescript
app.get("/download/:file(*)", (req, res) => {
  const file = req.params.file;
  const fileLocation = path.join(__dirname + "/uploads/", file);
  res.redirect("/downloads/" + file);
});
```

在上面的代码中，我们定义了一个到 `/download/:file(*)` 的 `GET` 路由。 `:file` 参数表示要下载的文件的名称。 `__dirname` 变量包含当前目录的路径。 `fileLocation` 变量包含要下载的文件的路径。 `res.redirect()` 方法用于将用户重定向到 `/downloads/` + `file`。

我们还可以使用 `res.json()` 方法发送 JSON 响应：

```typescript
app.get("/download/:file(*)", (req, res) => {
  const file = req.params.file;
  const fileLocation = path.join(__dirname + "/uploads/", file);
  res.json({
    message: "File downloaded successfully",
    file: file
  });
});
```

在上面的代码中，我们定义了一个到 `/download/:file(*)` 的 `GET` 路由。 `:file` 参数表示要下载的文件的名称。 `__dirname` 变量包含当前目录的路径。 `fileLocation` 变量包含要下载的文件的路径。 `res.json()` 方法用于发送 JSON 响应。