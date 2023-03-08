---
title: 将 TypeScript 与 Stripe 集成以进行支付
description: 
published: true
date: 2023-02-05T01:55:47.715Z
tags: 
editor: markdown
dateCreated: 2023-02-05T01:55:42.288Z
---

> 本文已使用 **Google Cloud Translation API 自动翻译**。
某些文档最好以原文阅读。{.is-info}



- [Integrating TypeScript with Stripe for Payments***English** document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-stripe-for-payments)
{.links-list}


# 将 TypeScript 与 Stripe 集成以进行支付

[Stripe](https://stripe.com/) 是处理信用卡支付的流行平台。它提供了一个[简单的 API](https://stripe.com/docs/api)，可以集成到 Web 应用程序中以接受付款。

TypeScript 是 JavaScript 的类型化超集，可编译为纯 JavaScript。它可以与各种 JavaScript 框架一起使用，以提供类型安全并提高开发人员的工作效率。

在本文中，我们将了解如何将 TypeScript 与 Stripe 集成以处理付款。我们将使用 [`stripe-typescript`](https://www.npmjs.com/package/stripe-typescript) NPM 包，它是 Stripe API 的 TypeScript 声明文件。

## 设置条纹

首先，我们需要创建一个 Stripe 帐户并获取我们的 API 密钥。我们可以通过访问 [Stripe 网站](https://stripe.com/) 并单击“开始”按钮来完成此操作。

![条纹网站](https://i.imgur.com/jjKsTGi.png)

在下一页，我们需要提供我们的电子邮件地址、选择密码并同意 Stripe 服务条款。

![条纹注册](https://i.imgur.com/ouae71z.png)

创建帐户后，我们可以登录并转到“开发人员”部分。在“开发人员”部分，我们可以在“API 密钥”选项卡下找到我们的 API 密钥。

![条纹 API 密钥](https://i.imgur.com/pZFg8bv.png)

我们需要复制“密钥”并将其保存在安全的地方。稍后我们将在设置 TypeScript 项目时使用此密钥。

## 设置 TypeScript 项目

现在我们已经设置了 Stripe 帐户，我们可以创建我们的 TypeScript 项目。我们将使用 [`create-react-app`](https://create-react-app.dev/) 工具来设置一个简单的 React 应用程序。

首先，我们需要安装 create-react-app 工具。我们可以使用 `npm` 来做到这一点：

```
npm install -g create-react-app
```

一旦安装了 create-react-app 工具，我们就可以创建我们的 React 项目了：

```
create-react-app stripe-typescript
```

这将为我们的 React 项目创建一个名为 `stripe-typescript` 的新目录。我们可以进入这个目录并启动开发服务器：

```
cd stripe-typescript
npm start
```

这将启动开发服务器并在我们的浏览器中打开 React 应用程序。

## 安装 `stripe-typescript` 包

现在我们已经设置了 React 项目，我们可以安装 `stripe-typescript` 包。我们可以使用 `npm` 来做到这一点：

```
npm install stripe-typescript
```

这将在我们的项目中安装 `stripe-typescript` 包。

## 配置 `stripe-typescript` 包

安装 `stripe-typescript` 包后，我们需要配置它。我们可以通过在项目的根目录中创建一个 `stripe.config.js` 文件来做到这一点，其中包含以下内容：

```javascript
module.exports = {
  apiKey: '<your Stripe secret key>',
};
```

将 `<your Stripe secret key>` 替换为我们之前从 Stripe 帐户复制的“Secret key”。

## 创建 Stripe 支付表单

现在我们已经安装并配置了 `stripe-typescript` 包，我们可以使用它来创建 Stripe 支付表单。为此，我们将在 src/components/PaymentForm.tsx 中创建一个新的 PaymentForm 组件，其内容如下：

```typescript
import * as React from 'react';
import { CardElement, injectStripe } from 'react-stripe-elements';

class PaymentForm extends React.Component {
  public state = {
    error: '',
  };

  public async submit(ev: React.FormEvent<HTMLFormElement>) {
    ev.preventDefault();

    try {
      const response = await this.props.stripe.createToken();
      console.log(response);
    } catch (error) {
      this.setState({
        error: error.message,
      });
    }
  }

  public render() {
    return (
      <form onSubmit={ev => this.submit(ev)}>
        <CardElement />
        <button type="submit">Pay</button>
        {this.state.error && <p>{this.state.error}</p>}
      </form>
    );
  }
}

export default injectStripe(PaymentForm);
```

这个 `PaymentForm` 组件呈现一个 `<form>` 元素，其中包含 `react-stripe-elements` 包中的 `<CardElement>` 元素。 `<CardElement>` 元素呈现一个信用卡输入元素，用于收集用户的信用卡详细信息。

`submit` 方法用于提交付款表单。此方法调用 `stripe.createToken` 方法来创建 Stripe 令牌。然后可以使用此令牌对信用卡收费。

## 渲染支付表单

现在我们已经创建了我们的 PaymentForm 组件，我们需要渲染它。我们可以通过修改 `src/App.tsx` 中的 `App` 组件来呈现 `PaymentForm` 组件来做到这一点：

```typescript
import * as React from 'react';
import PaymentForm from './components/PaymentForm';

function App() {
  return (
    <div className="App">
      <PaymentForm />
    </div>
  );
}

export default App;
```

现在，如果我们回到我们的浏览器，我们应该看到付款表格：

![付款方式](https://i.imgur.com/QBKMJj7.png)

## 信用卡充值

现在我们已经设置了付款表格，我们可以用它来对信用卡收费。我们将通过修改 `PaymentForm` 组件中的 `submit` 方法来调用 `stripe.charges.create` 方法来做到这一点：

```typescript
public async submit(ev: React.FormEvent<HTMLFormElement>) {
  ev.preventDefault();

  try {
    const { token } = await this.props.stripe.createToken({
      name: 'Test name',
    });

    await this.props.stripe.charges.create({
      amount: 1000,
      currency: 'usd',
      description: 'Test charge',
      source: token.id,
    });
  } catch (error) {
    this.setState({
      error: error.message,
    });
  }
}
```

这将从信用卡中扣除 10 美元。

## 测试支付表单

我们可以使用 [Stripe 测试卡](https://stripe.com/docs/testing# cards) 来测试我们的支付表单。我们可以使用下面的卡号：`4242 4242 4242 4242`。

如果我们输入此卡号并提交表单，我们应该会在浏览器控制台中看到一条成功消息：

![充值成功](https://i.imgur.com/xyQLbNw.png)

## 资源

- [条纹网站](https://stripe.com/)
- [条纹 API](https://stripe.com/docs/api)
- [`stripe-typescript` NPM 包](https://www.npmjs.com/package/stripe-typescript)
- [`react-stripe-elements` NPM 包](https://www.npmjs.com/package/react-stripe-elements)
- [`create-react-app` 工具](https://create-react-app.dev/)