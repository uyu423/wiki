---
title: Integrating TypeScript with SendGrid for Email Notifications
description: 
published: true
date: 2023-02-24T01:32:25.658Z
tags: 
editor: markdown
dateCreated: 2023-02-24T01:32:18.752Z
---

- [이메일 알림을 위해 TypeScript와 SendGrid 통합***Korean** document is available*](/ko/Knowledge-base/TypeScript/integrating-typescript-with-sendgrid-for-email-notifications)
{.links-list}


# Integrating TypeScript with SendGrid for Email Notifications

Developers often need to send email notifications as part of their applications. SendGrid is a popular service for sending emails, and their API can be integrated with TypeScript applications.

## Setting up SendGrid

The first step is to [create a SendGrid account](https://sendgrid.com/pricing/). Once you have an account, you'll need to [create an API key](https://app.sendgrid.com/settings/api_keys). Be sure to give your API key a name and select **Full Access** for the permissions.

## Installing the SendGrid TypeScript SDK

Now that you have a SendGrid account and API key, you can install the TypeScript SDK. The SDK will allow you to interact with the SendGrid API in your TypeScript code.

```typescript
npm install @sendgrid/client --save
```

## Sending an Email Notification

With the SDK installed, you can now write TypeScript code to send email notifications. The code below shows how to send a basic email notification.

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

In the code above, we first imported the SendGrid SDK. Then, we initialized the SDK with our SendGrid API key. Next, we created a message object with the recipient, sender, subject, and text of our email. Finally, we used the SDK to send the message.

## Handling Errors

It's important to handle errors when sending email notifications. The code below shows how to catch and handle errors when using the SendGrid SDK.

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

In the code above, we added a catch block to handle errors. In the catch block, we log the error and also the error response from the SendGrid API. This is helpful for debugging purposes.

## External Resources

- [SendGrid Documentation](https://sendgrid.com/docs)
- [SendGrid TypeScript SDK](https://www.npmjs.com/package/@sendgrid/client)