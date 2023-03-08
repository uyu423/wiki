---
title: Integración de TypeScript con Stripe para pagos
description: 
published: true
date: 2023-02-05T01:55:47.715Z
tags: 
editor: markdown
dateCreated: 2023-02-05T01:55:42.291Z
---

> Esta página se **tradujo automáticamente con la API de traducción de Google Cloud**.
Algunas páginas se pueden leer mejor en su totalidad.{.is-info}



- [Integrating TypeScript with Stripe for Payments***English** document is available*](/en/Knowledge-base/TypeScript/integrating-typescript-with-stripe-for-payments)
{.links-list}


# Integración de TypeScript con Stripe para pagos

[Stripe](https://stripe.com/) es una plataforma popular para procesar pagos con tarjeta de crédito. Ofrece una [API simple](https://stripe.com/docs/api) que se puede integrar en aplicaciones web para aceptar pagos.

TypeScript es un superconjunto escrito de JavaScript que se compila en JavaScript simple. Se puede usar con varios marcos de JavaScript para proporcionar seguridad de tipo y mejorar la productividad del desarrollador.

En este artículo, veremos cómo integrar TypeScript con Stripe para procesar pagos. Usaremos el paquete NPM [`stripe-typescript`](https://www.npmjs.com/package/stripe-typescript), que es un archivo de declaración de TypeScript para la API de Stripe.

## Configuración de la raya

Primero, necesitamos crear una cuenta de Stripe y obtener nuestras claves API. Podemos hacer esto yendo al [sitio web de Stripe](https://stripe.com/) y haciendo clic en el botón "Comenzar".

![Sitio web de Stripe](https://i.imgur.com/jjKsTGi.png)

En la página siguiente, debemos proporcionar nuestra dirección de correo electrónico, elegir una contraseña y aceptar los términos de servicio de Stripe.

![Stripe registrarse](https://i.imgur.com/ouae71z.png)

Una vez que hemos creado nuestra cuenta, podemos iniciar sesión e ir a la sección "Desarrolladores". En la sección "Desarrolladores", podemos encontrar nuestras claves API en la pestaña "Claves API".

![Claves API de bandas](https://i.imgur.com/pZFg8bv.png)

Necesitamos copiar la "Clave secreta" y guardarla en un lugar seguro. Usaremos esta clave más adelante cuando configuremos nuestro proyecto TypeScript.

## Configuración del proyecto TypeScript

Ahora que tenemos configurada nuestra cuenta de Stripe, podemos crear nuestro proyecto TypeScript. Usaremos la herramienta [`create-react-app`](https://create-react-app.dev/) para configurar una aplicación React simple.

Primero, necesitamos instalar la herramienta `create-react-app`. Podemos hacer esto con `npm`:

```
npm install -g create-react-app
```

Una vez instalada la herramienta `create-react-app`, podemos crear nuestro proyecto React:

```
create-react-app stripe-typescript
```

Esto creará un nuevo directorio llamado `stripe-typescript` con nuestro proyecto React. Podemos cambiar a este directorio e iniciar el servidor de desarrollo:

```
cd stripe-typescript
npm start
```

Esto iniciará el servidor de desarrollo y abrirá la aplicación React en nuestro navegador.

## Instalación del paquete `stripe-typescript`

Ahora que tenemos configurado nuestro proyecto React, podemos instalar el paquete `stripe-typescript`. Podemos hacer esto con `npm`:

```
npm install stripe-typescript
```

Esto instalará el paquete `stripe-typescript` en nuestro proyecto.

## Configurando el paquete `stripe-typescript`

Una vez instalado el paquete `stripe-typescript`, debemos configurarlo. Podemos hacer esto creando un archivo `stripe.config.js` en la raíz de nuestro proyecto con los siguientes contenidos:

```javascript
module.exports = {
  apiKey: '<your Stripe secret key>',
};
```

Reemplaza `<tu clave secreta de Stripe>` con la "clave secreta" que copiamos anteriormente de nuestra cuenta de Stripe.

## Creando un formulario de pago de Stripe

Ahora que tenemos el paquete `stripe-typescript` instalado y configurado, podemos usarlo para crear un formulario de pago de Stripe. Haremos esto creando un nuevo componente `PaymentForm` en `src/components/PaymentForm.tsx` con los siguientes contenidos:

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

Este componente `PaymentForm` representa un elemento `<form>` con un elemento `<CardElement>` del paquete `react-stripe-elements`. El elemento `<CardElement>` representa un elemento de entrada de tarjeta de crédito que recopila los detalles de la tarjeta de crédito del usuario.

El método "enviar" se utiliza para enviar el formulario de pago. Este método llama al método `stripe.createToken` para crear un token Stripe. Este token se puede usar para cargar la tarjeta de crédito.

## Representación del formulario de pago

Ahora que hemos creado nuestro componente `PaymentForm`, necesitamos renderizarlo. Podemos hacer esto modificando el componente `App` en `src/App.tsx` para representar el componente `PaymentForm`:

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

Ahora, si volvemos a nuestro navegador, deberíamos ver el formulario de pago:

![Forma de pago](https://i.imgur.com/QBKMJj7.png)

## Cargar la tarjeta de crédito

Ahora que tenemos nuestro formulario de pago configurado, podemos usarlo para cargar una tarjeta de crédito. Haremos esto modificando el método `submit` en nuestro componente `PaymentForm` para llamar al método `stripe.charges.create`:

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

Esto cargará la tarjeta de crédito $10.

## Probando el formulario de pago

Podemos probar nuestro formulario de pago usando una [tarjeta de prueba de Stripe](https://stripe.com/docs/testing# cards). Podemos utilizar el siguiente número de tarjeta: `4242 4242 4242 4242`.

Si ingresamos este número de tarjeta y enviamos el formulario, deberíamos ver un mensaje de éxito en la consola del navegador:

![Cargo exitoso](https://i.imgur.com/xyQLbNw.png)

## Recursos

- [Sitio web de Stripe](https://stripe.com/)
- [API de banda](https://stripe.com/docs/api)
- [paquete NPM `stripe-typescript`](https://www.npmjs.com/package/stripe-typescript)
- [paquete NPM `react-stripe-elements`](https://www.npmjs.com/package/react-stripe-elements)
- [herramienta `create-react-app`](https://create-react-app.dev/)