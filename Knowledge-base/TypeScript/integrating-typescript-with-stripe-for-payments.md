---
title: Stripe for Payments와 TypeScript 통합
description: 
published: true
date: 2023-02-05T01:55:47.715Z
tags: 
editor: markdown
dateCreated: 2023-02-05T01:55:42.287Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Integrating TypeScript with Stripe for Payments***English** document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-stripe-for-payments)
{.links-list}


# Stripe for Payments와 TypeScript 통합

[Stripe](https://stripe.com/)는 신용 카드 결제를 처리하는 인기 있는 플랫폼입니다. 결제 수락을 위해 웹 애플리케이션에 통합할 수 있는 [간단한 API](https://stripe.com/docs/api)를 제공합니다.

TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript 상위 집합입니다. 유형 안전성을 제공하고 개발자 생산성을 향상시키기 위해 다양한 JavaScript 프레임워크와 함께 사용할 수 있습니다.

이 기사에서는 결제 처리를 위해 TypeScript를 Stripe과 통합하는 방법을 살펴봅니다. Stripe API용 TypeScript 선언 파일인 [`stripe-typescript`](https://www.npmjs.com/package/stripe-typescript) NPM 패키지를 사용하겠습니다.

## 스트라이프 설정

먼저 Stripe 계정을 생성하고 API 키를 받아야 합니다. [Stripe 웹사이트](https://stripe.com/)로 이동하여 "시작하기" 버튼을 클릭하면 됩니다.

![스트라이프 홈페이지](https://i.imgur.com/jjKsTGi.png)

다음 페이지에서 이메일 주소를 제공하고 비밀번호를 선택하고 Stripe 서비스 약관에 동의해야 합니다.

![스트라이프 가입하기](https://i.imgur.com/ouae71z.png)

계정을 만들면 로그인하여 "개발자" 섹션으로 이동할 수 있습니다. "개발자" 섹션의 "API 키" 탭에서 API 키를 찾을 수 있습니다.

![스트라이프 API 키](https://i.imgur.com/pZFg8bv.png)

"비밀 키"를 복사하여 안전한 곳에 저장해야 합니다. 나중에 TypeScript 프로젝트를 설정할 때 이 키를 사용합니다.

## TypeScript 프로젝트 설정

이제 Stripe 계정이 설정되었으므로 TypeScript 프로젝트를 만들 수 있습니다. [`create-react-app`](https://create-react-app.dev/) 도구를 사용하여 간단한 React 애플리케이션을 설정하겠습니다.

먼저 `create-react-app` 도구를 설치해야 합니다. 우리는 `npm`으로 이것을 할 수 있습니다:

```
npm install -g create-react-app
```

`create-react-app` 도구가 설치되면 React 프로젝트를 만들 수 있습니다.

```
create-react-app stripe-typescript
```

이렇게 하면 React 프로젝트와 함께 `stripe-typescript`라는 새 디렉토리가 생성됩니다. 이 디렉토리로 변경하고 개발 서버를 시작할 수 있습니다.

```
cd stripe-typescript
npm start
```

이렇게 하면 개발 서버가 시작되고 브라우저에서 React 애플리케이션이 열립니다.

## `stripe-typescript` 패키지 설치

이제 React 프로젝트가 설정되었으므로 `stripe-typescript` 패키지를 설치할 수 있습니다. 우리는 `npm`으로 이것을 할 수 있습니다:

```
npm install stripe-typescript
```

이렇게 하면 프로젝트에 `stripe-typescript` 패키지가 설치됩니다.

## `stripe-typescript` 패키지 구성

`stripe-typescript` 패키지가 설치되면 구성해야 합니다. 다음 내용으로 프로젝트의 루트에 `stripe.config.js` 파일을 생성하여 이를 수행할 수 있습니다.

```javascript
module.exports = {
  apiKey: '<your Stripe secret key>',
};
```

`<your Stripe 비밀 키>`를 이전에 Stripe 계정에서 복사한 "비밀 키"로 바꿉니다.

## Stripe 결제 양식 만들기

이제 `stripe-typescript` 패키지를 설치 및 구성했으므로 이를 사용하여 Stripe 결제 양식을 만들 수 있습니다. 다음 내용으로 `src/components/PaymentForm.tsx`에 새 `PaymentForm` 구성 요소를 생성하여 이를 수행합니다.

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

이 `PaymentForm` 구성요소는 `react-stripe-elements` 패키지의 `<CardElement>` 요소로 `<form>` 요소를 렌더링합니다. `<CardElement>` 요소는 사용자로부터 신용 카드 정보를 수집하는 신용 카드 입력 요소를 렌더링합니다.

'제출' 방법은 결제 양식을 제출하는 데 사용됩니다. 이 메소드는 스트라이프 토큰을 생성하기 위해 `stripe.createToken` 메소드를 호출합니다. 그런 다음 이 토큰을 사용하여 신용 카드를 청구할 수 있습니다.

## 결제 양식 렌더링

이제 `PaymentForm` 컴포넌트를 생성했으므로 렌더링해야 합니다. `PaymentForm` 구성 요소를 렌더링하기 위해 `src/App.tsx`에서 `App` 구성 요소를 수정하여 이를 수행할 수 있습니다.

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

이제 브라우저로 돌아가면 결제 양식이 표시됩니다.

![결제 방법](https://i.imgur.com/QBKMJj7.png)

## 신용 카드 충전

이제 결제 양식이 설정되었으므로 이를 사용하여 신용 카드를 청구할 수 있습니다. `PaymentForm` 구성 요소의 `submit` 메소드를 수정하여 `stripe.charges.create` 메소드를 호출하여 이를 수행합니다.

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

이렇게 하면 신용 카드에 $10가 청구됩니다.

## 결제 양식 테스트

[Stripe 테스트 카드](https://stripe.com/docs/testing# cards)를 사용하여 결제 양식을 테스트할 수 있습니다. 다음 카드 번호를 사용할 수 있습니다: `4242 4242 4242 4242`.

이 카드 번호를 입력하고 양식을 제출하면 브라우저 콘솔에 성공 메시지가 표시됩니다.

![충전성공](https://i.imgur.com/xyQLbNw.png)

## 자원

- [스트라이프 홈페이지](https://stripe.com/)
- [스트라이프 API](https://stripe.com/docs/api)
- [`stripe-typescript` NPM 패키지](https://www.npmjs.com/package/stripe-typescript)
- [`react-stripe-elements` NPM 패키지](https://www.npmjs.com/package/react-stripe-elements)
- [`create-react-app` 도구](https://create-react-app.dev/)