---
title: 이메일 알림을 위해 TypeScript와 SendGrid 통합
description: 
published: true
date: 2023-02-24T01:32:20.149Z
tags: 
editor: markdown
dateCreated: 2023-02-24T01:32:18.749Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Integrating TypeScript with SendGrid for Email Notifications***English** document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-sendgrid-for-email-notifications)
{.links-list}


# 이메일 알림을 위해 TypeScript를 SendGrid와 통합

개발자는 종종 애플리케이션의 일부로 이메일 알림을 보내야 합니다. SendGrid는 이메일 전송에 널리 사용되는 서비스이며 해당 API는 TypeScript 애플리케이션과 통합될 수 있습니다.

## SendGrid 설정

첫 번째 단계는 [SendGrid 계정 생성](https://sendgrid.com/pricing/)입니다. 계정이 있으면 [API 키를 생성](https://app.sendgrid.com/settings/api_keys)해야 합니다. API 키에 이름을 지정하고 권한에 대해 **전체 액세스**를 선택해야 합니다.

## SendGrid TypeScript SDK 설치하기

이제 SendGrid 계정과 API 키가 있으므로 TypeScript SDK를 설치할 수 있습니다. SDK를 사용하면 TypeScript 코드에서 SendGrid API와 상호 작용할 수 있습니다.

```typescript
npm install @sendgrid/client --save
```

## 이메일 알림 보내기

SDK가 설치되면 이제 TypeScript 코드를 작성하여 이메일 알림을 보낼 수 있습니다. 아래 코드는 기본 이메일 알림을 보내는 방법을 보여줍니다.

```typescript
import * as SendGrid from '@sendgrid/client';

const sendgrid = SendGrid.SendGridApi.v3({
  apiKey: 'your-sendgrid-api-key',
});

const message = {
  to: 'example@example.com',
  from: 'example@example.com',
  subject: 'Hello, world!',
  text: 'This is a test email from my TypeScript application.',
};

sendgrid.send(message).then(() => {
  console.log('Email sent successfully!');
}).catch((error) => {
  console.error(error);
});
```

위의 코드에서 먼저 SendGrid SDK를 가져왔습니다. 그런 다음 SendGrid API 키로 SDK를 초기화했습니다. 다음으로 수신자, 발신자, 제목 및 이메일 텍스트로 메시지 객체를 생성했습니다. 마지막으로 SDK를 사용하여 메시지를 보냈습니다.

## 오류 처리

이메일 알림을 보낼 때 오류를 처리하는 것이 중요합니다. 아래 코드는 SendGrid SDK를 사용할 때 오류를 포착하고 처리하는 방법을 보여줍니다.

```typescript
import * as SendGrid from '@sendgrid/client';

const sendgrid = SendGrid.SendGridApi.v3({
  apiKey: 'your-sendgrid-api-key',
});

const message = {
  to: 'example@example.com',
  from: 'example@example.com',
  subject: 'Hello, world!',
  text: 'This is a test email from my TypeScript application.',
};

sendgrid.send(message).then(() => {
  console.log('Email sent successfully!');
}).catch((error) => {
  console.error(error);
  if (error.response) {
    console.error(error.response.body);
  }
});
```

위의 코드에서 오류를 처리하기 위해 catch 블록을 추가했습니다. catch 블록에서 오류와 SendGrid API의 오류 응답을 기록합니다. 이는 디버깅 목적에 유용합니다.

## 외부 리소스

- [SendGrid 문서](https://sendgrid.com/docs)
- [SendGrid TypeScript SDK](https://www.npmjs.com/package/@sendgrid/client)