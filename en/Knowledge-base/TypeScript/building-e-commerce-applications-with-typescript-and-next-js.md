---
title: Building E-Commerce Applications with TypeScript and Next.js
description: 
published: true
date: 2023-02-25T22:33:16.939Z
tags: 
editor: markdown
dateCreated: 2023-02-25T22:33:09.956Z
---

- [TypeScript 및 Next.js로 전자 상거래 애플리케이션 구축***Korean** document is available*](/ko/Knowledge-base/TypeScript/building-e-commerce-applications-with-typescript-and-next-js)
{.links-list}


# Building E-Commerce Applications with TypeScript and Next.js

Developers are often tasked with creating ecommerce applications that are fast, reliable, and easy to maintain. TypeScript and Next.js can be used to build such applications with ease. In this article, we will take a look at how to use TypeScript and Next.js to build ecommerce applications.

## What is TypeScript?

TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. It offers features such as type annotations, interfaces, classes, and modules. TypeScript is a powerful tool that can help developers write type-safe code and avoid common programming errors.

## What is Next.js?

Next.js is a React framework that makes it easy to create server-side rendered React applications. It offers features such as automatic code splitting, static site generation, and server-side rendering. Next.js is a great choice for building ecommerce applications because it makes it easy to create fast, scalable, and SEO-friendly applications.

## Building an Ecommerce Application with TypeScript and Next.js

Now that we know what TypeScript and Next.js are, let's take a look at how to use them to build an ecommerce application.

We will start by scaffolding a Next.js application using the create-next-app CLI.

```
npx create-next-app my-app
```

Once the application has been scaffolded, we can install the TypeScript dependencies and create a tsconfig.json file.

```
npm install --save-dev typescript @types/react @types/node
```

```
touch tsconfig.json
```

The tsconfig.json file specifies the TypeScript options for the project. We will set the "target" to "esnext" and the "jsx" to "preserve". This will allow us to use TypeScript with Next.js and preserve the JSX.

```
{
  "compilerOptions": {
    "target": "esnext",
    "jsx": "preserve"
  }
}
```

Now that we have TypeScript configured, we can create a TypeScript file for our component. We will name our component "MyComponent.tsx".

```
touch components/MyComponent.tsx
```

```
import React from 'react';

const MyComponent = () => {
  return <div>Hello, world!</div>;
};

export default MyComponent;
```

This is a simple functional React component that renders a div element with the text "Hello, world!".

Now that we have our component, we can render it in our Next.js application. We will do this in the "pages/index.js" file.

```
import React from 'react';
import MyComponent from '../components/MyComponent';

const IndexPage = () => {
  return (
    <div>
      <MyComponent />
    </div>
  );
};

export default IndexPage;
```

If we run our application, we should see the "Hello, world!" text on the page.

Now that we have a basic Next.js application with TypeScript, we can start building our ecommerce application.

We will start by creating a " products" directory in our project. In this directory, we will create a " products.json" file that will contain the data for our products.

```
mkdir products
touch products/products.json
```

```
[
  {
    "id": "1",
    "name": "Product 1",
    "price": 9.99
  },
  {
    "id": "2",
    "name": "Product 2",
    "price": 19.99
  },
  {
    "id": "3",
    "name": "Product 3",
    "price": 29.99
  }
]
```

Next, we will create a " Product" component that will display the data for each product. We will name our component " Product.tsx" and place it in the " components" directory.

```
touch components/Product.tsx
```

```
import React from 'react';

interface ProductProps {
  name: string;
  price: number;
}

const Product: React.FC<ProductProps> = ({ name, price }) => {
  return (
    <div>
      <h1>{name}</h1>
      <p>{price}</p>
    </div>
  );
};

export default Product;
```

This component accepts a " name" and " price" props and renders a div element with the product name and price.

Now that we have our " Product" component, we can use it to display our products. We will do this in the " pages/index.js" file.

```
import React from 'react';
import Product from '../components/Product';
import products from '../products/products.json';

const IndexPage = () => {
  return (
    <div>
      {products.map(product => (
        <Product key={product.id} name={product.name} price={product.price} />
      ))}
    </div>
  );
};

export default IndexPage;
```

In this file, we are importing the " Product" component and the " products.json" file. We are then using the " map" method to loop over the products and render a " Product" component for each product.

If we run our application, we should see a list of products on the page.

Next, we will add a " Add to Cart" button to our " Product" component. We will do this by adding a new prop called " onAddToCart" to our " Product" component.

```
import React from 'react';

interface ProductProps {
  name: string;
  price: number;
  onAddToCart: (product: Product) => void;
}

const Product: React.FC<ProductProps> = ({ name, price, onAddToCart }) => {
  return (
    <div>
      <h1>{name}</h1>
      <p>{price}</p>
      <button onClick={() => onAddToCart({ name, price })}>Add to Cart</button>
    </div>
  );
};

export default Product;
```

In this file, we are adding a new prop called " onAddToCart" to our " Product" component. This prop accepts a function that will be called when the " Add to Cart" button is clicked. The function will be passed the product data.

Now that we have our " Add to Cart" button, we need to add a way to track the products that have been added to the cart. We will do this by creating a " useCart" hook. This hook will manage the state of the cart and expose methods for adding and removing items from the cart.

```
touch src/hooks/useCart.ts
```

```
import { useState } from 'react';

interface Product {
  name: string;
  price: number;
}

interface CartItem {
  product: Product;
  quantity: number;
}

interface UseCart {
  cartItems: CartItem[];
  total: number;
  addItem: (product: Product) => void;
  removeItem: (product: Product) => void;
}

const useCart = (): UseCart => {
  const [cartItems, setCartItems] = useState<CartItem[]>([]);

  const addItem = (product: Product) => {
    const existingCartItem = cartItems.find(
      cartItem => cartItem.product.name === product.name
    );

    if (existingCartItem) {
      setCartItems(
        cartItems.map(cartItem =>
          cartItem.product.name === product.name
            ? { ...cartItem, quantity: cartItem.quantity + 1 }
            : cartItem
        )
      );
    } else {
      setCartItems([...cartItems, { product, quantity: 1 }]);
    }
  };

  const removeItem = (product: Product) => {
    const existingCartItem = cartItems.find(
      cartItem => cartItem.product.name === product.name
    );

    if (existingCartItem && existingCartItem.quantity === 1) {
      setCartItems(cartItems.filter(cartItem => cartItem.product.name !== product.name));
    } else if (existingCartItem) {
      setCartItems(
        cartItems.map(cartItem =>
          cartItem.product.name === product.name
            ? { ...cartItem, quantity: cartItem.quantity - 1 }
            : cartItem
        )
      );
    }
  };

  const total = cartItems.reduce((acc, cartItem) => acc + cartItem.quantity * cartItem.product.price, 0);

  return { cartItems, total, addItem, removeItem };
};

export default useCart;
```

This hook exposes the " cartItems" state, a " total" computed property, and methods for " adding" and " removing" items from the cart.

Now that we have our " useCart" hook, we can use it in our " pages/index.js" file.

```
import React from 'react';
import Product from '../components/Product';
import products from '../products/products.json';
import useCart from '../src/hooks/useCart';

const IndexPage = () => {
  const { cartItems, total, addItem, removeItem } = useCart();

  return (
    <div>
      {products.map(product => (
        <Product
          key={product.id}
          name={product.name}
          price={product.price}
          onAddToCart={addItem}
          onRemoveFromCart={removeItem}
        />
      ))}
      <p>Total: {total}</p>
      <ul>
        {cartItems.map(cartItem => (
          <li key={cartItem.product.name}>
            {cartItem.quantity} {cartItem.product.name}
          </li>
        ))}
      </ul>
    </div>
  );
};

export default IndexPage;
```

In this file, we are using the " useCart" hook to add state management and methods for adding and removing items from the cart. We are then passing the " addItem" and " removeItem" methods to our " Product" component as props.

Finally, we are displaying the total price of the items in the cart and a list of the items in the cart.

If we run our application, we should see our products on the page with " Add to Cart" buttons. If we click on the " Add to Cart" button, we should see the item added to the cart.

This is a basic ecommerce application built with TypeScript and Next.js. In a real-world application, you would likely want to add features such as a shopping cart, checkout process, and payment gateway.

## Conclusion

TypeScript and Next.js can be used to build fast, reliable, and easy to maintain ecommerce applications. In this article, we looked at how to use TypeScript and Next.js to build an ecommerce application.