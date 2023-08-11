# JSX

## 학습 키워드

- React에서 JSX를 사용하는 목적
- Syntactic sugar
- React.createElement
- React Element
- React StrictMode
- VDOM(Virtual DOM)이란?
  - DOM이란?
  - DOM과 Virtual DOM의 차이
- Reconciliation(재조정) 과정은 무엇인가?

## JSX란?

> 자바스크립트의 **확장 문법**이다.

> 브라우저에서 실행하기 전에 코드가 번들링되는 과정에서 **바벨을 사용하여 일반 자바스크립트 형태의 코드로 변환**된다.

> 자바스크립트의 공식적인 문법이라고 할 수는 없다.

📚 JSX는 XML처럼 작성된 부분을 React.createElement을 쓰는 JavaScript 코드로 변환한다.
중괄호를 써서 JavaScript 코드를 그대로 쓸 수 있고, 결국은 JavaScript 코드와 1:1로 매칭된다.

## React에서 JSX를 사용하는 목적

> **자바스크립트에서 HTML을 작성하듯이 비슷하게 작성할 수 있도록 해 주는 것**이 JSX의 가장 큰 장점이자, 이를 사용하는 이유이다.

## **Syntatic Sugar**

> 프로그래밍 언어 차원에서 제공되는 논리적으로 간결하게 표현하는 것이며, 중복되는 로직을 간결하게 표현하기 위해 나타나게 되었다.

[Syntatic Sugar란?](https://nesoy.github.io/articles/2019-12/Syntactic-sugar)

## React.createElement

> **JSX** 대신 그냥 React.createElement를 써서 React Element 트리를 갱신하는데 쓸 수 있다.

JSX 코드

```jsx
<div>
  <p>Count: {count}!</p>
  <button type="button" onClick={() => setCount(count + 1)}>
    Increase
  </button>
</div>
```

변환된 JS 코드

```jsx
React.createElement(
  "div",
  null,
  React.createElement("p", null, "Count: ", count, "!"),
  React.createElement(
    "button",
    { type: "button", onClick: () => setCount(count + 1) },
    "Increase"
  )
);
```

## React

> **StrictMode**는 애플리케이션 내의 잠재적인 문제를 알아내기 위한 도구이며, 개발 모드에서만 활성화되기 때문에, 프로덕션 빌드에는 영향을 끼치지 않는다.

```jsx
import React from "react";

function ExampleApplication() {
  return (
    <div>
      <Header />
      <React.StrictMode>
        <div>
          <ComponentOne />
          <ComponentTwo />
        </div>
      </React.StrictMode>
      <Footer />
    </div>
  );
}
```

### 장점

- [안전하지 않은 생명주기를 사용하는 컴포넌트 발견](https://ko.legacy.reactjs.org/docs/strict-mode.html#identifying-unsafe-lifecycles)
- [레거시 문자열 ref 사용에 대한 경고](https://ko.legacy.reactjs.org/docs/strict-mode.html#warning-about-legacy-string-ref-api-usage)
- [권장되지 않는 findDOMNode 사용에 대한 경고](https://ko.legacy.reactjs.org/docs/strict-mode.html#warning-about-deprecated-finddomnode-usage)
- [예상치 못한 부작용 검사](https://ko.legacy.reactjs.org/docs/strict-mode.html#detecting-unexpected-side-effects)
- [레거시 context API 검사](https://ko.legacy.reactjs.org/docs/strict-mode.html#detecting-legacy-context-api)
- [Ensuring reusable state](https://ko.legacy.reactjs.org/docs/strict-mode.html#ensuring-reusable-state)

## VDOM(Virtual DOM)이란?

> **Virtual DOM**은 실제 DOM과 같은 내용을 담고 있는 복사본이라고 생각하시면 쉽다. 복사본은 실제 DOM이 아닌 JS 객체형태로 메모리 안에 저장되어 있다.

### DOM

> **문서 객체 모델**(The Document Object Model, 이하 DOM) 은 HTML, XML 문서의 프로그래밍 interface 이며, HTML문서를 브라우저가 이해할 수 있도록 만든 Tree 자료구조이다.

### DOM과 Virtual DOM의 차이

> **Real** **DOM**은 element의 자식노드가 추가되면 전체 문서가 갱신되지만
> **Virtual DOM**은 버퍼 역활을 해줌으로서 **Real DOM**을 추상화한 **DOM**과 비교하여
> 변경점만 **Real** **DOM**에 적용하여 전체 문서가 갱신되지 않는다.

## Reconciliation(재조정) 과정은 무엇인가?

> 리액트의 컴포넌트에서 prop이나 state가 변경될 때, 직전에 렌더링된 요소(element)와 새로 반환된 요소를 비교하여 실제 DOM을 업데이트 할지 말지 결정해야 한다. 이때 두 element가 일치하지 않으면 리액트는 새로운 요소로 DOM을 업데이트 하는데, 이러한 프로세스를 **reconciliation**이라고 한다.

### **비교 알고리즘 (Diffing Algorithm)**

> 두 컴퍼넌트를 비교할 때 React는 두 루트 요소부터 비교한다. 이 동작은 루트 요소의 타입에 따라 다르다.

### 유의사항

- 두 컴퍼넌트가 교체하는 상황에서는 그 둘을 같은 타입으로 만드는 것이 더 효율적이다.
- key값을 선정할 때는, 형제 사이에서만 유일하면 되고, 전역에서 유일한 value 일 필요는 없다.
- 배열의 인덱스는 key로 사용하지 않는 것이 좋다. 항목들이 재배열되면, key값이 변경될 수 있기 때문이다.
- key는 변하지 않고, 예상 가능하면서, 유일해야 한다. (Math.random() 같은 걸 key로 쓰면 안됨)

## 2주차 후기
