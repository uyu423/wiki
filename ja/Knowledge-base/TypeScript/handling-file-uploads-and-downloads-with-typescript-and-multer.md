---
title: TypeScript と Multer を使用したファイルのアップロードとダウンロードの処理
description: 
published: true
date: 2023-02-17T18:15:41.252Z
tags: 
editor: markdown
dateCreated: 2023-01-30T23:36:52.575Z
---

> この記事は **Google Cloud Translation APIを使用した自動翻訳**です。
いくつかの文書は原文を読むのに良いかもしれません。{.is-info}
- [Handling File Uploads and Downloads with TypeScript and Multer***English** version of this document is available*](/en/Knowledge-base/TypeScript/handling-file-uploads-and-downloads-with-typescript-and-multer)
{.links-list}


#TypeScriptとMulterによるファイルのアップロードとダウンロードの処理

## ファイルのアップロードとダウンロードは、Web アプリケーションの一般的な作業です。 Multer は、主にファイルのアップロードに使用される multipart/form-data を処理するための Node.js ミドルウェアです。 TypeScriptは、コードに入力された属性を提供するJavaScriptの親セットです。この記事では、MulterでTypeScriptを使用してファイルをアップロードする方法について説明します。

まず、必要な依存関係をインストールします。次のコマンドを使用してMulterをインストールできます。

```
npm install multer
```

TypeScriptは、次のコマンドを使用してインストールできます。

```
npm install typescript
```

依存関係がインストールされたら、TypeScriptファイルを作成し、名前を `index.ts`として指定します。 Multerのインスタンスを初期化することから始めましょう。

```typescript
import multer from "multer";

const upload = multer();
```

ここで作成された `upload` オブジェクトはファイルアップロードプロセスを処理するのに役立ちます。 `multer`関数は、ファイルアップロードの設定に使用できるオプションオブジェクトを受け入れます。たとえば、次のようにアップロードされたファイルの宛先を指定できます。

```typescript
const upload = multer({dest: "uploads/"});
```

この場合、ファイルは `uploads`ディレクトリにアップロードされます。アップロードしたファイルの名前を指定することもできます。

```typescript
const upload = multer({
  dest: "uploads/",
  fileFilter: function(req, file, cb) {
    const ext = path.extname（file.originalname）;
    if (ext !== ".jpg" && ext !== ".jpeg" && ext !== ".png") {
      return cb(new Error("Only jpg, jpeg, and png files are allowed"));
    }
    cb（null、true）;
  },
  filename: function(req, file, cb) {
    cb(null, file.fieldname + "-" + Date.now());
  }
}）;
```

上記のコードでは、`jpg`、`jpeg`、および`png`ファイルのみを許可するように指定しました。また、アップロードされたファイルの名前を「fieldname-timestamp」と指定しました。ここで、「fieldname」はフォームフィールドの名前、「timestamp」は現在のタイムスタンプです。

`upload`オブジェクトが設定されたら、それを使ってファイルのアップロードを処理できます。たとえば、次のようにファイルのアップロードを処理するパスを定義できます。

```typescript
app.post("/upload", upload.single("avatar"), (req, res) => {
  res.send("File uploaded successfully");
}）;
```

上記のコードで `/upload` への `POST` パスを定義しました。 `upload.single()` メソッドは、単一のファイルアップロードを処理するために使用されます。 `avatar`フィールドは、ファイルを含むフォームフィールドの名前を指定するために使用されます。 `req`オブジェクトは `req.file`にアップロードされたファイルを含みます。コールバック関数では、ファイルが正常にアップロードされたという応答を送信するだけです。

また、 `upload.array()` メソッドを使用して複数のファイルアップロードを処理することもできます。

```typescript
app.post("/upload", upload.array("photos", 12), (req, res) => {
  res.send("Files uploaded successfully");
}）;
```

上記のコードで最大12個のファイルをアップロードできるように指定しました。 「photos」フィールドは、ファイルを含むフォームフィールドの名前を指定するために使用されます。 `req.files`配列にはアップロードされたファイルが含まれています。

混合フィールドを処理するために `upload.fields()` メソッドを使うこともできます。

```typescript
app.post（
  "/upload",
  upload.fields（[
    { name: "avatar", maxCount: 1 },
    { name: "photos", maxCount: 8 }
  ]),
  (req, res) => {
    res.send("Files uploaded successfully");
  }
）;
```

上記のコードで `/upload` への `POST` パスを定義しました。 `upload.fields()` メソッドは混合フィールドを処理するために使用されます。 `avatar`フィールドと`photos`フィールドを処理することを指定しました。 「アバター」フィールドには最大1つのファイルを含めることができ、「写真」フィールドには最大8つのファイルを含めることができます。

ファイルを含まないフィールドを処理するために `upload.none()` メソッドを使うこともできます:

```typescript
app.post("/profile", upload.none(), (req, res) => {
  // req.body contains the text fields
  res.send("Profile updated successfully");
}）;
```

上記のコードで `/profile` への `POST` パスを定義しました。 `upload.none()` メソッドは、ファイルを含まないフィールドを処理するために使用されます。 `req.body`オブジェクトにはテキストフィールドが含まれています。

また、 `upload.any()` メソッドを使用して任意の型のフィールドを処理できます。

```typescript
app.post("/contact", upload.any(), (req, res) => {
  // req.body contains the text fields and the files
  res.send("Message sent successfully");
}）;
```

上記のコードで `/contact` への `POST` パスを定義しました。 `upload.any()` メソッドは、すべての型のフィールドを処理するために使用されます。 `req.body`オブジェクトにはテキストフィールドとファイルが含まれています。

## ファイルのダウンロードは、Webアプリケーションのもう一つの一般的な作業です。 TypeScriptとMulterを使用してファイルをダウンロードできます。たとえば、 `uploads`ディレクトリに `avatar.jpg`というファイルがあるとしましょう。次のように、このファイルをダウンロードするパスを定義できます。

```typescript
app.get("/download/:file(*)", (req, res) => {
  const file = req.params.file;
  const fileLocation = path.join(__dirname + "/uploads/", file);
  res.download(fileLocation, file);
}）;
```

上記のコードで `/download/:file(*)` への `GET` パスを定義しました。 `：file`パラメータはダウンロードするファイルの名前を示します。 `__dirname`変数は現在のディレクトリへのパスを含みます。 `fileLocation`変数には、ダウンロードするファイルのパスが含まれています。 `res.download()` メソッドはファイルをダウンロードするために使用されます。

ファイルを送信するために `res.sendFile()` メソッドを使うこともできます:

```typescript
app.get("/download/:file(*)", (req, res) => {
  const file = req.params.file;
  const fileLocation = path.join(__dirname + "/uploads/", file);
  res.sendFile(fileLocation);
}）;
```

上記のコードで `/download/:file(*)` への `GET` パスを定義しました。 `：file`パラメータはダウンロードするファイルの名前を示します。 `__dirname`変数は現在のディレクトリへのパスを含みます。 `fileLocation`変数には、ダウンロードするファイルのパスが含まれています。 `res.sendFile()` メソッドはファイルを送るのに使われます。

また、 `res.attachment()` メソッドを使用してファイルを添付ファイルとして送信することもできます。

```typescript
app.get("/download/:file(*)", (req, res) => {
  const file = req.params.file;
  const fileLocation = path.join(__dirname + "/uploads/", file);
  res.attachment（fileLocation）;
}）;
```

上記のコードで `/download/:file(*)` への `GET` パスを定義しました。 `：file`パラメータはダウンロードするファイルの名前を示します。 `__dirname`変数は現在のディレクトリへのパスを含みます。 `fileLocation`変数には、ダウンロードするファイルのパスが含まれています。 `res.attachment()` メソッドは、ファイルを添付ファイルとして送信するために使用されます。

また、 `res.redirect()` メソッドを使用してユーザーを別のページにリダイレクトすることもできます。

```typescript
app.get("/download/:file(*)", (req, res) => {
  const file = req.params.file;
  const fileLocation = path.join(__dirname + "/uploads/", file);
  res.redirect("/downloads/" + file);
}）;
```

上記のコードで `/download/:file(*)` への `GET` パスを定義しました。 `：file`パラメータはダウンロードするファイルの名前を示します。 `__dirname`変数は現在のディレクトリへのパスを含みます。 `fileLocation`変数には、ダウンロードするファイルのパスが含まれています。 `res.redirect()` メソッドは、ユーザーを `/downloads/` + `file` にリダイレクトするために使用されます。

また、 `res.json()` メソッドを使って JSON レスポンスを送信することもできます。

```typescript
app.get("/download/:file(*)", (req, res) => {
  const file = req.params.file;
  const fileLocation = path.join(__dirname + "/uploads/", file);
  res.json({
    message: "File downloaded successfully",
    file: file
  }）;
}）;
```

上記のコードで `/download/:file(*)` への `GET` パスを定義しました。 `：file`パラメータはダウンロードするファイルの名前を示します。 `__dirname`変数は現在のディレクトリへのパスを含みます。 `fileLocation`変数には、ダウンロードするファイルのパスが含まれています。 `res.json()` メソッドは JSON 応答を送信するために使用されます。