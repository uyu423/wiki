---
title: React.js 시작하기
description: 
published: true
date: 2023-01-29T20:01:14.775Z
tags: 
editor: markdown
dateCreated: 2023-01-29T20:01:14.775Z
---


# React.js 시작하기

React는 사용자 인터페이스 구축에 널리 사용되는 JavaScript 라이브러리입니다. React를 처음 사용하는 경우 시작하는 데 유용한 온라인 리소스를 많이 찾을 수 있습니다.

이 블로그 게시물에서는 React의 기본 사항 중 일부를 다루어 자신만의 React 애플리케이션 구축을 시작할 수 있도록 합니다.

## 리액트란?

React는 사용자 인터페이스를 구축하기 위한 JavaScript 라이브러리입니다. React를 사용하면 코드를 쉽게 읽고 유지 관리할 수 있도록 재사용 가능한 구성 요소를 만들 수 있습니다.

React는 선언적 프로그래밍 언어입니다. 즉, UI가 어떻게 보여야 하는지 설명할 수 있습니다. React는 데이터가 변경될 때 UI 업데이트를 처리합니다.

## 리액트를 사용하는 이유?

React는 코드를 더 읽기 쉽고 유지 관리하기 쉽게 만들기 때문에 사용자 인터페이스를 구축하는 데 널리 사용되는 선택입니다. React는 변경된 UI 부분만 업데이트하기 때문에 효율적입니다.

## 시작하기

React를 시작하려면 HTML과 CSS에 대한 기본적인 이해가 필요합니다. 이러한 기술을 배우는 데 도움이 되는 많은 리소스를 온라인에서 찾을 수 있습니다.

HTML 및 CSS에 대한 기본적인 이해가 있으면 텍스트 편집기를 사용하여 `.js` 확장자를 가진 파일을 생성하여 React 애플리케이션을 생성할 수 있습니다.

`.js` 파일에서 React 코드를 작성합니다. React와 같은 JavaScript 라이브러리를 사용하여 코드를 더 쉽게 작성할 수 있습니다.

React는 JavaScript 라이브러리이므로 `.js` 파일에 React 라이브러리를 포함해야 합니다. `.js` 파일에 다음 코드를 추가하면 됩니다.

```
import React from 'react';
```

React 라이브러리를 가져오면 `React.createClass` 메서드를 사용하여 React 구성 요소를 만들 수 있습니다.

React 컴포넌트는 UI의 일부를 설명하는 코드 조각입니다. 예를 들어 양식 입력을 렌더링하는 구성 요소를 만들 수 있습니다.

React 구성 요소를 만들려면 `React.createClass` 메서드를 사용해야 합니다. 이 메서드는 개체를 인수로 사용합니다. 개체에는 `render` 메서드가 있어야 합니다. `render` 메서드는 구성 요소가 무엇을 렌더링해야 하는지에 대한 설명을 반환해야 합니다.

예를 들어 다음 코드는 양식 입력을 렌더링하는 React 구성 요소를 만듭니다.

```
import React from 'react';

const FormInput = React.createClass({
  render() {
    return (
      <input type="text" />
    );
  }
});
```

React 구성 요소를 만든 후에는 `ReactDOM.render` 메서드를 사용하여 화면에 렌더링할 수 있습니다.

`ReactDOM.render` 메서드는 두 가지 인수를 사용합니다.

- 렌더링하려는 React 구성 요소입니다.
- React 구성 요소를 렌더링하려는 DOM의 요소입니다.

예를 들어 다음 코드는 `FormInput` 구성 요소를 `<body>` 요소로 렌더링합니다.

```
import React from 'react';
import ReactDOM from 'react-dom';

const FormInput = React.createClass({
  render() {
    return (
      <input type="text" />
    );
  }
});

ReactDOM.render(
  <FormInput />,
  document.body
);
```

## 소품 추가

React 구성 요소는 구성 요소에 전달할 수 있는 특성인 props를 사용할 수 있습니다. 소품은 구성 요소의 동작을 사용자 정의하는 데 사용됩니다.

예를 들어 `type` 소품을 사용하는 `FormInput` 구성 요소를 만들 수 있습니다. `type` 소품은 `FormInput` 구성 요소에 의해 렌더링되는 `<input>` 요소의 `type` 속성을 설정하는 데 사용됩니다.

`type` 소품을 사용하는 `FormInput` 구성 요소를 만들려면 다음 코드를 작성합니다.

```
import React from 'react';

const FormInput = React.createClass({
  render() {
    return (
      <input type={this.props.type} />
    );
  }
});
```

그런 다음 `FormInput` 컴포넌트를 렌더링하고 `type` prop을 전달할 수 있습니다.

```
import React from 'react';
import ReactDOM from 'react-dom';

const FormInput = React.createClass({
  render() {
    return (
      <input type={this.props.type} />
    );
  }
});

ReactDOM.render(
  <FormInput type="text" />,
  document.body
);
```

## 상태 추가

React 구성 요소는 변경할 수 있는 데이터인 상태를 가질 수 있습니다. 상태는 구성 요소의 동작을 사용자 지정하는 데 사용할 수 있는 정보를 저장하는 데 사용됩니다.

예를 들어, `value` prop을 받아 state에 저장하는 `FormInput` 컴포넌트를 생성할 수 있습니다. `value` 소품은 `FormInput` 구성요소에 의해 렌더링되는 `<input>` 요소의 `value` 속성을 설정하는 데 사용됩니다.

`value` prop을 가져와 상태에 저장하는 `FormInput` 구성 요소를 만들려면 다음 코드를 작성합니다.

```
import React from 'react';

const FormInput = React.createClass({
  getInitialState() {
    return {
      value: ''
    };
  },
  
  render() {
    return (
      <input type="text" value={this.state.value} />
    );
  }
});
```

그런 다음 `FormInput` 구성 요소를 렌더링하고 여기에 `value` prop을 전달할 수 있습니다.

```
import React from 'react';
import ReactDOM from 'react-dom';

const FormInput = React.createClass({
  getInitialState() {
    return {
      value: ''
    };
  },
  
  render() {
    return (
      <input type="text" value={this.state.value} />
    );
  }
});

ReactDOM.render(
  <FormInput value="Hello!" />,
  document.body
);
```

## 이벤트 처리기 추가

React 구성 요소에는 이벤트가 발생할 때 호출되는 함수인 이벤트 핸들러가 있을 수 있습니다. 이벤트 처리기는 사용자 입력을 처리하는 데 사용됩니다.

예를 들어, `value` prop을 받아 state에 저장하는 `FormInput` 컴포넌트를 생성할 수 있습니다. `value` 소품은 `FormInput` 구성요소에 의해 렌더링되는 `<input>` 요소의 `value` 속성을 설정하는 데 사용됩니다.

또한 `FormInput` 구성 요소에 `onChange` 이벤트 핸들러를 추가할 수 있습니다. `onChange` 이벤트 핸들러는 사용자가 `<input>` 요소에 입력할 때 호출됩니다.

`value` prop을 가져와 상태에 저장하는 `FormInput` 구성 요소를 만들려면 다음 코드를 작성합니다.

```
import React from 'react';

const FormInput = React.createClass({
  getInitialState() {
    return {
      value: ''
    };
  },
  
  handleChange(event) {
    this.setState({
      value: event.target.value
    });
  },
  
  render() {
    return (
      <input type="text" value={this.state.value} onChange={this.handleChange} />
    );
  }
});
```

그런 다음 `FormInput` 구성 요소를 렌더링하고 여기에 `value` prop을 전달할 수 있습니다.

```
import React from 'react';
import ReactDOM from 'react-dom';

const FormInput = React.createClass({
  getInitialState() {
    return {
      value: ''
    };
  },
  
  handleChange(event) {
    this.setState({
      value: event.target.value
    });
  },
  
  render() {
    return (
      <input type="text" value={this.state.value} onChange={this.handleChange} />
    );
  }
});

ReactDOM.render(
  <FormInput value="Hello!" />,
  document.body
);
```

## 자녀 추가

React 구성 요소는 부모 구성 요소 내부에서 렌더링되는 다른 React 구성 요소인 자식을 가질 수 있습니다.

예를 들어 `FormInput` 구성 요소를 렌더링하는 `Form` 구성 요소를 만들 수 있습니다. `Form` 구성 요소는 부모 구성 요소가 되고 `FormInput` 구성 요소는 자식 구성 요소가 됩니다.

`FormInput` 구성 요소를 렌더링하는 `Form` 구성 요소를 만들려면 다음 코드를 작성합니다.

```
import React from 'react';

const Form = React.createClass({
  render() {
    return (
      <form>
        <FormInput />
      </form>
    );
  }
});
```

그런 다음 `Form` 구성 요소를 렌더링할 수 있습니다.

```
import React from 'react';
import ReactDOM from 'react-dom';

const Form = React.createClass({
  render() {
    return (
      <form>
        <FormInput />
      </form>
    );
  }
});

ReactDOM.render(
  <Form />,
  document.body
);
```

## 결론

이 블로그 게시물에서는 React의 기본 사항 중 일부를 다루어 자신만의 React 애플리케이션 구축을 시작할 수 있도록 했습니다. React 구성 요소를 만드는 방법, React 구성 요소에 props 및 상태를 추가하는 방법, React 구성 요소에 이벤트 핸들러 및 자식을 추가하는 방법을 다뤘습니다.