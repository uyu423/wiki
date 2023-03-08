---
title: Handling File Uploads and Downloads with TypeScript and Multer
description: 
published: true
date: 2023-02-17T18:15:39.832Z
tags: 
editor: markdown
dateCreated: 2023-01-30T23:36:52.575Z
---

- [TypeScript 및 Multer로 파일 업로드 및 다운로드 처리***Korean** version of this document is available*](/ko/Knowledge-base/TypeScript/handling-file-uploads-and-downloads-with-typescript-and-multer)
{.links-list}
- [TypeScript と Multer を使用したファイルのアップロードとダウンロードの処理***Japanese** version of this document is available*](/ja/Knowledge-base/TypeScript/handling-file-uploads-and-downloads-with-typescript-and-multer)
{.links-list}
- [使用 TypeScript 和 Multer 处理文件上传和下载***Chinese Simplified** version of this document is available*](/zh/Knowledge-base/TypeScript/handling-file-uploads-and-downloads-with-typescript-and-multer)
{.links-list}


# Handling File Uploads and Downloads with TypeScript and Multer

## Uploading and downloading files is a common task for web applications. Multer is a Node.js middleware for handling multipart/form-data, which is primarily used for uploading files. TypeScript is a superset of JavaScript that provides typed nature to your code. In this article, we'll see how to use TypeScript with Multer to upload files.

We'll first install the required dependencies. You can use the following command to install Multer:

```
npm install multer
```

TypeScript can be installed using the following command:

```
npm install typescript
```

Once the dependencies are installed, let's create a TypeScript file and name it `index.ts`. We'll start by initializing an instance of Multer:

```typescript
import multer from "multer";

const upload = multer();
```

The `upload` object created here is going to help us handle the file upload process. The `multer` function accepts an options object, which can be used to configure the file upload. For example, we can specify the destination for uploaded files as follows:

```typescript
const upload = multer({dest: "uploads/"});
```

In this case, the files will be uploaded to the `uploads` directory. We can also specify the name of the uploaded file:

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

In the code above, we've specified that only `jpg`, `jpeg`, and `png` files are allowed. We've also specified that the name of the uploaded file should be `fieldname-timestamp`, where `fieldname` is the name of the form field and `timestamp` is the current timestamp.

Once the `upload` object is configured, we can use it to handle file uploads. For example, we can define a route to handle file uploads as follows:

```typescript
app.post("/upload", upload.single("avatar"), (req, res) => {
  res.send("File uploaded successfully");
});
```

In the code above, we've defined a `POST` route to `/upload`. The `upload.single()` method is used to process a single file upload. The `avatar` field is used to specify the name of the form field that contains the file. The `req` object contains the uploaded file in `req.file`. In the callback function, we're just sending a response saying that the file was uploaded successfully.

We can also use the `upload.array()` method to process multiple file uploads:

```typescript
app.post("/upload", upload.array("photos", 12), (req, res) => {
  res.send("Files uploaded successfully");
});
```

In the code above, we've specified that up to 12 files can be uploaded. The `photos` field is used to specify the name of the form field that contains the files. The `req.files` array contains the uploaded files.

We can also use the `upload.fields()` method to process mixed fields:

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

In the code above, we've defined a `POST` route to `/upload`. The `upload.fields()` method is used to process mixed fields. We've specified that we want to process an `avatar` field and a `photos` field. The `avatar` field can have a maximum of 1 file and the `photos` field can have a maximum of 8 files.

We can also use the `upload.none()` method to process fields that don't contain files:

```typescript
app.post("/profile", upload.none(), (req, res) => {
  // req.body contains the text fields
  res.send("Profile updated successfully");
});
```

In the code above, we've defined a `POST` route to `/profile`. The `upload.none()` method is used to process fields that don't contain files. The `req.body` object contains the text fields.

We can also use the `upload.any()` method to process any type of field:

```typescript
app.post("/contact", upload.any(), (req, res) => {
  // req.body contains the text fields and the files
  res.send("Message sent successfully");
});
```

In the code above, we've defined a `POST` route to `/contact`. The `upload.any()` method is used to process any type of field. The `req.body` object contains the text fields and the files.

## Downloading files is another common task for web applications. We can use TypeScript and Multer to download files. For example, let's say we have a file named ` avatar.jpg` in the `uploads` directory. We can define a route to download this file as follows:

```typescript
app.get("/download/:file(*)", (req, res) => {
  const file = req.params.file;
  const fileLocation = path.join(__dirname + "/uploads/", file);
  res.download(fileLocation, file);
});
```

In the code above, we've defined a `GET` route to `/download/:file(*)`. The `:file` parameter represents the name of the file to be downloaded. The `__dirname` variable contains the path of the current directory. The `fileLocation` variable contains the path of the file to be downloaded. The `res.download()` method is used to download the file.

We can also use the `res.sendFile()` method to send the file:

```typescript
app.get("/download/:file(*)", (req, res) => {
  const file = req.params.file;
  const fileLocation = path.join(__dirname + "/uploads/", file);
  res.sendFile(fileLocation);
});
```

In the code above, we've defined a `GET` route to `/download/:file(*)`. The `:file` parameter represents the name of the file to be downloaded. The `__dirname` variable contains the path of the current directory. The `fileLocation` variable contains the path of the file to be downloaded. The `res.sendFile()` method is used to send the file.

We can also use the `res.attachment()` method to send the file as an attachment:

```typescript
app.get("/download/:file(*)", (req, res) => {
  const file = req.params.file;
  const fileLocation = path.join(__dirname + "/uploads/", file);
  res.attachment(fileLocation);
});
```

In the code above, we've defined a `GET` route to `/download/:file(*)`. The `:file` parameter represents the name of the file to be downloaded. The `__dirname` variable contains the path of the current directory. The `fileLocation` variable contains the path of the file to be downloaded. The `res.attachment()` method is used to send the file as an attachment.

We can also use the `res.redirect()` method to redirect the user to another page:

```typescript
app.get("/download/:file(*)", (req, res) => {
  const file = req.params.file;
  const fileLocation = path.join(__dirname + "/uploads/", file);
  res.redirect("/downloads/" + file);
});
```

In the code above, we've defined a `GET` route to `/download/:file(*)`. The `:file` parameter represents the name of the file to be downloaded. The `__dirname` variable contains the path of the current directory. The `fileLocation` variable contains the path of the file to be downloaded. The `res.redirect()` method is used to redirect the user to `/downloads/` + `file`.

We can also use the `res.json()` method to send a JSON response:

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

In the code above, we've defined a `GET` route to `/download/:file(*)`. The `:file` parameter represents the name of the file to be downloaded. The `__dirname` variable contains the path of the current directory. The `fileLocation` variable contains the path of the file to be downloaded. The `res.json()` method is used to send a JSON response.