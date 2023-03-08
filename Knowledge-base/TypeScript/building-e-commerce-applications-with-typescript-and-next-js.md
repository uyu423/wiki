---
title: TypeScript 및 Next.js로 전자 상거래 애플리케이션 구축
description: 
published: true
date: 2023-02-25T22:33:11.408Z
tags: 
editor: markdown
dateCreated: 2023-02-25T22:33:09.964Z
---

> 이 문서는 **Google Cloud Translation API를 사용해 자동 번역**되었습니다.
어떤 문서는 원문을 읽는게 나을 수도 있습니다.{.is-info}



- [Building E-Commerce Applications with TypeScript and Next.js***English** document is available*](/en/Knowledge-base/TypeScript/building-e-commerce-applications-with-typescript-and-next-js)
{.links-list}


# TypeScript와 Next.js로 전자 상거래 애플리케이션 구축

개발자는 종종 빠르고 안정적이며 유지 관리하기 쉬운 전자 상거래 애플리케이션을 만드는 임무를 맡습니다. TypeScript 및 Next.js를 사용하여 이러한 애플리케이션을 쉽게 구축할 수 있습니다. 이 기사에서는 TypeScript와 Next.js를 사용하여 전자상거래 애플리케이션을 구축하는 방법을 살펴보겠습니다.

## 타입스크립트란?

TypeScript는 일반 JavaScript로 컴파일되는 유형이 지정된 JavaScript 상위 집합입니다. 유형 주석, 인터페이스, 클래스 및 모듈과 같은 기능을 제공합니다. TypeScript는 개발자가 안전한 코드를 작성하고 일반적인 프로그래밍 오류를 방지하는 데 도움이 되는 강력한 도구입니다.

## Next.js가 무엇인가요?

Next.js는 서버 측 렌더링된 React 애플리케이션을 쉽게 만들 수 있는 React 프레임워크입니다. 자동 코드 분할, 정적 사이트 생성 및 서버 측 렌더링과 같은 기능을 제공합니다. Next.js는 빠르고 확장 가능하며 SEO 친화적인 애플리케이션을 쉽게 만들 수 있기 때문에 전자 상거래 애플리케이션 구축에 탁월한 선택입니다.

## TypeScript 및 Next.js로 전자상거래 애플리케이션 구축

TypeScript와 Next.js가 무엇인지 알았으니 이제 전자 상거래 애플리케이션을 구축하는 데 사용하는 방법을 살펴보겠습니다.

create-next-app CLI를 사용하여 Next.js 애플리케이션을 스캐폴딩하는 것으로 시작하겠습니다.

```
npx create-next-app my-app
```

애플리케이션이 스캐폴드되면 TypeScript 종속성을 설치하고 tsconfig.json 파일을 생성할 수 있습니다.

```
npm install --save-dev typescript @types/react @types/node
```

```
touch tsconfig.json
```

tsconfig.json 파일은 프로젝트에 대한 TypeScript 옵션을 지정합니다. "target"을 "esnext"로 설정하고 "jsx"를 "preserve"로 설정합니다. 이를 통해 Next.js와 함께 TypeScript를 사용하고 JSX를 보존할 수 있습니다.

```
{
  "compilerOptions": {
    "target": "esnext",
    "jsx": "preserve"
  }
}
```

이제 TypeScript를 구성했으므로 구성 요소에 대한 TypeScript 파일을 만들 수 있습니다. 구성 요소 이름을 "MyComponent.tsx"로 지정합니다.

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

이것은 "Hello, world!"라는 텍스트가 있는 div 요소를 렌더링하는 간단한 기능적 React 구성 요소입니다.

이제 컴포넌트가 있으므로 Next.js 애플리케이션에서 렌더링할 수 있습니다. "pages/index.js" 파일에서 이 작업을 수행합니다.

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

애플리케이션을 실행하면 "Hello, world!" 페이지의 텍스트.

이제 TypeScript를 사용한 기본 Next.js 애플리케이션이 있으므로 전자상거래 애플리케이션 구축을 시작할 수 있습니다.

프로젝트에 "products" 디렉토리를 만드는 것으로 시작하겠습니다. 이 디렉토리에서 제품에 대한 데이터를 포함할 " products.json" 파일을 생성합니다.

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

다음으로 각 제품에 대한 데이터를 표시할 "제품" 구성 요소를 만듭니다. 구성 요소 이름을 " Product.tsx"로 지정하고 " 구성 요소" 디렉터리에 배치합니다.

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

이 구성 요소는 " name" 및 " price" 소품을 허용하고 제품 이름 및 가격으로 div 요소를 렌더링합니다.

이제 "제품" 구성 요소가 있으므로 이를 사용하여 제품을 표시할 수 있습니다. "pages/index.js" 파일에서 이 작업을 수행합니다.

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

이 파일에서 " Product" 구성 요소와 " products.json" 파일을 가져옵니다. 그런 다음 " map" 메서드를 사용하여 제품을 반복하고 각 제품에 대한 " Product" 구성 요소를 렌더링합니다.

애플리케이션을 실행하면 페이지에 제품 목록이 표시됩니다.

다음으로 "제품" 구성 요소에 "장바구니에 추가" 버튼을 추가합니다. " Product" 구성 요소에 " onAddToCart"라는 새 소품을 추가하여 이 작업을 수행합니다.

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

이 파일에서 " 제품" 구성 요소에 " onAddToCart"라는 새 소품을 추가하고 있습니다. 이 소품은 "장바구니에 추가" 버튼을 클릭할 때 호출되는 함수를 허용합니다. 기능은 제품 데이터를 전달합니다.

이제 "카트에 추가" 버튼이 있으므로 카트에 추가된 제품을 추적하는 방법을 추가해야 합니다. "useCart" 후크를 생성하여 이를 수행합니다. 이 후크는 카트의 상태를 관리하고 카트에서 항목을 추가 및 제거하는 방법을 노출합니다.

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

이 후크는 " cartItems" 상태, " total" 계산 속성, 카트에서 항목을 " 추가" 및 " 제거"하는 메서드를 노출합니다.

이제 "useCart" 후크가 있으므로 "pages/index.js" 파일에서 사용할 수 있습니다.

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

이 파일에서 "useCart" 후크를 사용하여 카트에서 항목을 추가하고 제거하기 위한 상태 관리 및 메서드를 추가합니다. 그런 다음 " addItem" 및 " removeItem" 메서드를 " Product" 구성 요소에 소품으로 전달합니다.

마지막으로 카트에 있는 항목의 총 가격과 카트에 있는 항목 목록을 표시합니다.

애플리케이션을 실행하면 "장바구니에 추가" 버튼이 있는 페이지에 제품이 표시되어야 합니다. "장바구니에 추가" 버튼을 클릭하면 항목이 카트에 추가된 것을 볼 수 있습니다.

이것은 TypeScript 및 Next.js로 구축된 기본 전자 상거래 애플리케이션입니다. 실제 애플리케이션에서는 장바구니, 체크아웃 프로세스 및 지불 게이트웨이와 같은 기능을 추가하려고 할 것입니다.

## 결론

TypeScript 및 Next.js를 사용하여 빠르고 안정적이며 유지 관리하기 쉬운 전자 상거래 애플리케이션을 구축할 수 있습니다. 이 기사에서는 TypeScript와 Next.js를 사용하여 전자상거래 애플리케이션을 구축하는 방법을 살펴보았습니다.