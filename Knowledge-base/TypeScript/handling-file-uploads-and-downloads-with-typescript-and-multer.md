---
title: TypeScript 및 Multer로 파일 업로드 및 다운로드 처리
description: 
published: true
date: 2023-02-17T18:15:38.393Z
tags: 
editor: markdown
dateCreated: 2023-01-30T23:36:52.573Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}
- [Handling File Uploads and Downloads with TypeScript and Multer***English** version of this document is available*](/en/Knowledge-base/TypeScript/handling-file-uploads-and-downloads-with-typescript-and-multer)
{.links-list}


# TypeScript 및 Multer로 파일 업로드 및 다운로드 처리

## 파일 업로드 및 다운로드는 웹 애플리케이션의 일반적인 작업입니다. Multer는 주로 파일 업로드에 사용되는 multipart/form-data를 처리하기 위한 Node.js 미들웨어입니다. TypeScript는 코드에 입력된 특성을 제공하는 JavaScript의 상위 집합입니다. 이 기사에서는 Multer와 함께 TypeScript를 사용하여 파일을 업로드하는 방법을 살펴보겠습니다.

먼저 필요한 종속성을 설치합니다. 다음 명령을 사용하여 Multer를 설치할 수 있습니다.

```
npm install multer
```

TypeScript는 다음 명령을 사용하여 설치할 수 있습니다.

```
npm install typescript
```

종속성이 설치되면 TypeScript 파일을 만들고 이름을 `index.ts`로 지정합니다. Multer의 인스턴스를 초기화하는 것으로 시작하겠습니다.

```typescript
import multer from "multer";

const upload = multer();
```

여기에서 생성된 `upload` 개체는 파일 업로드 프로세스를 처리하는 데 도움이 됩니다. `multer` 함수는 파일 업로드를 구성하는 데 사용할 수 있는 옵션 개체를 허용합니다. 예를 들어 다음과 같이 업로드된 파일의 대상을 지정할 수 있습니다.

```typescript
const upload = multer({dest: "uploads/"});
```

이 경우 파일은 `uploads` 디렉토리에 업로드됩니다. 업로드된 파일의 이름을 지정할 수도 있습니다.

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

위의 코드에서 `jpg`, `jpeg` 및 `png` 파일만 허용되도록 지정했습니다. 또한 업로드된 파일의 이름을 'fieldname-timestamp'로 지정했습니다. 여기서 'fieldname'은 양식 필드의 이름이고 'timestamp'는 현재 타임스탬프입니다.

`upload` 개체가 구성되면 이를 사용하여 파일 업로드를 처리할 수 있습니다. 예를 들어 다음과 같이 파일 업로드를 처리하는 경로를 정의할 수 있습니다.

```typescript
app.post("/upload", upload.single("avatar"), (req, res) => {
  res.send("File uploaded successfully");
});
```

위의 코드에서 `/upload`에 대한 `POST` 경로를 정의했습니다. `upload.single()` 메서드는 단일 파일 업로드를 처리하는 데 사용됩니다. `avatar` 필드는 파일을 포함하는 양식 필드의 이름을 지정하는 데 사용됩니다. `req` 객체는 `req.file`에 업로드된 파일을 포함합니다. 콜백 함수에서는 파일이 성공적으로 업로드되었다는 응답을 보내는 것뿐입니다.

또한 `upload.array()` 메서드를 사용하여 여러 파일 업로드를 처리할 수 있습니다.

```typescript
app.post("/upload", upload.array("photos", 12), (req, res) => {
  res.send("Files uploaded successfully");
});
```

위의 코드에서 최대 12개의 파일을 업로드할 수 있도록 지정했습니다. 'photos' 필드는 파일이 포함된 양식 필드의 이름을 지정하는 데 사용됩니다. `req.files` 배열에는 업로드된 파일이 포함됩니다.

혼합 필드를 처리하기 위해 `upload.fields()` 메서드를 사용할 수도 있습니다.

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

위의 코드에서 `/upload`에 대한 `POST` 경로를 정의했습니다. `upload.fields()` 메서드는 혼합 필드를 처리하는 데 사용됩니다. `avatar` 필드와 `photos` 필드를 처리하도록 지정했습니다. `아바타` 필드는 최대 1개의 파일을 포함할 수 있으며 `사진` 필드는 최대 8개의 파일을 포함할 수 있습니다.

파일을 포함하지 않는 필드를 처리하기 위해 `upload.none()` 메서드를 사용할 수도 있습니다:

```typescript
app.post("/profile", upload.none(), (req, res) => {
  // req.body contains the text fields
  res.send("Profile updated successfully");
});
```

위의 코드에서 `/profile`에 대한 `POST` 경로를 정의했습니다. `upload.none()` 메서드는 파일을 포함하지 않는 필드를 처리하는 데 사용됩니다. `req.body` 개체에는 텍스트 필드가 포함되어 있습니다.

또한 `upload.any()` 메서드를 사용하여 모든 유형의 필드를 처리할 수 있습니다.

```typescript
app.post("/contact", upload.any(), (req, res) => {
  // req.body contains the text fields and the files
  res.send("Message sent successfully");
});
```

위의 코드에서 `/contact`에 대한 `POST` 경로를 정의했습니다. `upload.any()` 메서드는 모든 유형의 필드를 처리하는 데 사용됩니다. `req.body` 개체에는 텍스트 필드와 파일이 포함되어 있습니다.

## 파일 다운로드는 웹 애플리케이션의 또 다른 일반적인 작업입니다. TypeScript와 Multer를 사용하여 파일을 다운로드할 수 있습니다. 예를 들어 `uploads` 디렉토리에 ` avatar.jpg`라는 파일이 있다고 가정해 보겠습니다. 다음과 같이 이 파일을 다운로드할 경로를 정의할 수 있습니다.

```typescript
app.get("/download/:file(*)", (req, res) => {
  const file = req.params.file;
  const fileLocation = path.join(__dirname + "/uploads/", file);
  res.download(fileLocation, file);
});
```

위의 코드에서 `/download/:file(*)`에 대한 `GET` 경로를 정의했습니다. `:file` 매개변수는 다운로드할 파일의 이름을 나타냅니다. `__dirname` 변수는 현재 디렉토리의 경로를 포함합니다. `fileLocation` 변수에는 다운로드할 파일의 경로가 포함됩니다. `res.download()` 메서드는 파일을 다운로드하는 데 사용됩니다.

파일을 보내기 위해 `res.sendFile()` 메서드를 사용할 수도 있습니다:

```typescript
app.get("/download/:file(*)", (req, res) => {
  const file = req.params.file;
  const fileLocation = path.join(__dirname + "/uploads/", file);
  res.sendFile(fileLocation);
});
```

위의 코드에서 `/download/:file(*)`에 대한 `GET` 경로를 정의했습니다. `:file` 매개변수는 다운로드할 파일의 이름을 나타냅니다. `__dirname` 변수는 현재 디렉토리의 경로를 포함합니다. `fileLocation` 변수에는 다운로드할 파일의 경로가 포함됩니다. `res.sendFile()` 메서드는 파일을 보내는 데 사용됩니다.

또한 `res.attachment()` 메서드를 사용하여 파일을 첨부 파일로 보낼 수 있습니다.

```typescript
app.get("/download/:file(*)", (req, res) => {
  const file = req.params.file;
  const fileLocation = path.join(__dirname + "/uploads/", file);
  res.attachment(fileLocation);
});
```

위의 코드에서 `/download/:file(*)`에 대한 `GET` 경로를 정의했습니다. `:file` 매개변수는 다운로드할 파일의 이름을 나타냅니다. `__dirname` 변수는 현재 디렉토리의 경로를 포함합니다. `fileLocation` 변수에는 다운로드할 파일의 경로가 포함됩니다. `res.attachment()` 메서드는 파일을 첨부 파일로 보내는 데 사용됩니다.

또한 `res.redirect()` 메서드를 사용하여 사용자를 다른 페이지로 리디렉션할 수 있습니다.

```typescript
app.get("/download/:file(*)", (req, res) => {
  const file = req.params.file;
  const fileLocation = path.join(__dirname + "/uploads/", file);
  res.redirect("/downloads/" + file);
});
```

위의 코드에서 `/download/:file(*)`에 대한 `GET` 경로를 정의했습니다. `:file` 매개변수는 다운로드할 파일의 이름을 나타냅니다. `__dirname` 변수는 현재 디렉토리의 경로를 포함합니다. `fileLocation` 변수에는 다운로드할 파일의 경로가 포함됩니다. `res.redirect()` 메서드는 사용자를 `/downloads/` + `file`로 리디렉션하는 데 사용됩니다.

또한 `res.json()` 메서드를 사용하여 JSON 응답을 보낼 수도 있습니다.

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

위의 코드에서 `/download/:file(*)`에 대한 `GET` 경로를 정의했습니다. `:file` 매개변수는 다운로드할 파일의 이름을 나타냅니다. `__dirname` 변수는 현재 디렉토리의 경로를 포함합니다. `fileLocation` 변수에는 다운로드할 파일의 경로가 포함됩니다. `res.json()` 메서드는 JSON 응답을 보내는 데 사용됩니다.