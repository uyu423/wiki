---
title: Integrating TypeScript with Stripe for Payments
description: 
published: true
date: 2023-02-05T01:55:44.030Z
tags: 
editor: markdown
dateCreated: 2023-02-05T01:55:42.294Z
---

- [Integración de TypeScript con Stripe para pagos***Spanish** document is available*](/es/Knowledge-base/TypeScript/integrating-typescript-with-stripe-for-payments)
{.links-list}
- [将 TypeScript 与 Stripe 集成以进行支付***Chinese Simplified** document is available*](/zh/Knowledge-base/TypeScript/integrating-typescript-with-stripe-for-payments)
{.links-list}
- [Stripe for Payments와 TypeScript 통합***Korean** document is available*](/ko/Knowledge-base/TypeScript/integrating-typescript-with-stripe-for-payments)
{.links-list}


# Integrating TypeScript with Stripe for Payments

[Stripe](https://stripe.com/) is a popular platform for processing credit card payments. It offers a [simple API](https://stripe.com/docs/api) that can be integrated into web applications for accepting payments.

TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. It can be used with various JavaScript frameworks to provide type safety and improve developer productivity.

In this article, we will see how to integrate TypeScript with Stripe for processing payments. We will use the [`stripe-typescript`](https://www.npmjs.com/package/stripe-typescript) NPM package, which is a TypeScript declaration file for the Stripe API.

## Setting up Stripe

First, we need to create a Stripe account and get our API keys. We can do this by going to the [Stripe website](https://stripe.com/) and clicking on the "Get started" button.

![Stripe website](https://i.imgur.com/jjKsTGi.png)

On the next page, we need to provide our email address, choose a password, and agree to the Stripe terms of service.

![Stripe sign up](https://i.imgur.com/ouae71z.png)

Once we have created our account, we can log in and go to the "Developers" section. In the "Developers" section, we can find our API keys under the "API keys" tab.

![Stripe API keys](https://i.imgur.com/pZFg8bv.png)

We need to copy the "Secret key" and save it somewhere safe. We will use this key later when we set up our TypeScript project.

## Setting up the TypeScript project

Now that we have our Stripe account set up, we can create our TypeScript project. We will use the [`create-react-app`](https://create-react-app.dev/) tool to set up a simple React application.

First, we need to install the `create-react-app` tool. We can do this with `npm`:

```
npm install -g create-react-app
```

Once the `create-react-app` tool is installed, we can create our React project:

```
create-react-app stripe-typescript
```

This will create a new directory called `stripe-typescript` with our React project. We can change into this directory and start the development server:

```
cd stripe-typescript
npm start
```

This will start the development server and open the React application in our browser.

## Installing the `stripe-typescript` package

Now that we have our React project set up, we can install the `stripe-typescript` package. We can do this with `npm`:

```
npm install stripe-typescript
```

This will install the `stripe-typescript` package in our project.

## Configuring the `stripe-typescript` package

Once the `stripe-typescript` package is installed, we need to configure it. We can do this by creating a `stripe.config.js` file in the root of our project with the following contents:

```javascript
module.exports = {
  apiKey: '<your Stripe secret key>',
};
```

Replace `<your Stripe secret key>` with the "Secret key" that we copied earlier from our Stripe account.

## Creating a Stripe payment form

Now that we have the `stripe-typescript` package installed and configured, we can use it to create a Stripe payment form. We will do this by creating a new `PaymentForm` component in `src/components/PaymentForm.tsx` with the following contents:

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

This `PaymentForm` component renders a `<form>` element with a `<CardElement>` element from the `react-stripe-elements` package. The `<CardElement>` element renders a credit card input element that collects the credit card details from the user.

The `submit` method is used to submit the payment form. This method calls the `stripe.createToken` method to create a Stripe token. This token can then be used to charge the credit card.

## Rendering the payment form

Now that we have created our `PaymentForm` component, we need to render it. We can do this by modifying the `App` component in `src/App.tsx` to render the `PaymentForm` component:

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

Now, if we go back to our browser, we should see the payment form:

![Payment form](https://i.imgur.com/QBKMJj7.png)

## Charging the credit card

Now that we have our payment form set up, we can use it to charge a credit card. We will do this by modifying the `submit` method in our `PaymentForm` component to call the `stripe.charges.create` method:

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

This will charge the credit card $10.

## Testing the payment form

We can test our payment form by using a [Stripe test card](https://stripe.com/docs/testing#cards). We can use the following card number: `4242 4242 4242 4242`.

If we enter this card number and submit the form, we should see a success message in the browser console:

![Successful charge](https://i.imgur.com/xyQLbNw.png)

## Resources

- [Stripe website](https://stripe.com/)
- [Stripe API](https://stripe.com/docs/api)
- [`stripe-typescript` NPM package](https://www.npmjs.com/package/stripe-typescript)
- [`react-stripe-elements` NPM package](https://www.npmjs.com/package/react-stripe-elements)
- [`create-react-app` tool](https://create-react-app.dev/)