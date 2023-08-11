# React의 Hook

## 학습 키워드

- React Hook 이란
- Hooks
  - useState
  - useEffect
  - useContext
  - useRef
  - useLayoutEffect
- React StrictMode 란

## React Hook 이란

> **Hook**은 React 버전 16.8부터 React요소로 새로 추가되었며, **Hook**을 이용하여 기존 Class 바탕의 코드를 작성할 필요 없이 상태 값과 여러 React의 가능을 사용할 수 있다.

## Hooks

### useState

> **useState**는 함수형 또는 클래스형 컴포넌트의 상태를 관리하고, 변경할 수 있도록 도와주는 하나의 React Hook이며, **useState는** 동적 데이터를 다루는 것, 컴포넌트별 고유한 상태 값, 변경 가능성(실시간 or 주기적 렌더링이 필요한 UI), 상태관리를 통한 컴포넌트 내부에 캡슐화를 활용하여 UI 업데이트 등에 사용된다.

```jsx
const [value, setValue] = useState(0);

//value는 저장된 값. 즉 useState(0)에서 0의 값을 갖게 된다.

//setValue의 경우 value 변경된 값을 저장할 수 있게 만들어 준다.
```

### useEffect

> **useEffect는** React component가 렌더링 될 때마다 특정 작업(**Sied effect**)을 실행할 수 있도록 하는 리액트 Hook이다. 여기서 **Side effect**는 **component**가 렌더링 된 이후에 비동기로 처리되어야 하는 부수적인 효과들을 뜻하며, 이러한 기능으로 인해 함수형 컴포넌트에서도 클래스형 컴포넌트에서 사용했던 생명주기 메서드를 사용할 수 있다.

```jsx
useEffect(() => {
  console.log('렌더링 될때마다 실행');
});

useEffect(() => {
  console.log('맨 처음 렌더링될 때 한 번만 실행');
}, []);

useEffect(() => {
  console.log(name);
  console.log('name이라는 값이 업데이트 될 때만 실행');
}, [name]);
```

### useContext

> **useContext**는 react에서 제공하는 훅으로, 하위 컴포넌트에게 context를 제공하는 hook이다. “context”란 직역하면 환경이라는 의미이지만, 여기서는 리액트에서는 각 컴포넌트가 참조할 수 있는 데이터 모음이라고 생각하면 된다.

```jsx
//App -> Middle -> End 순으로 props를 계속 전달 예시
import React from 'react';

function End({ text }: { text: string }) {
  return <div>{text}</div>;
}

function Middle({ text }: { text: string }) {
  return (
    <div>
      <End text={text} />
    </div>
  );
}

export default function App() {
  const text = 'Hello world';

  return (
    <div>
      <Middle text={text} />
    </div>
  );
}
```

```jsx
// useContext 사용 예시
import React, { createContext, useContext } from 'react';

const TextContext = createContext('Hello world');

function End() {
  const text = useContext(TextContext);
  return <div>{text}</div>;
}

function Middle() {
  return (
    <div>
      <End />
    </div>
  );
}

export default function App() {
  return (
    <div>
      <TextContext.Provider value={'Hello world'}>
        <Middle />
      </TextContext.Provider>
    </div>
  );
}
```

## useRef

> useRef란 원하는 특정 DOM을 직접 선택해서 컨트롤 할 수 있게 해주는 Hook이다
> 예를 들면 엘리먼트의 크기를 가져오거나 스타일 변경, 포커스 등의 작업을 해야할 때 useRef를 사용하면 된다.

```jsx
import { useRef } from 'react';

const App = () => {
  const ref = useRef();

  return <input type="text" name="keyword" ref={ref} />;
};

//button 클릭 시 input 값 초기화
import { useRef } from 'react';

const App = () => {
  const ref = useRef();

  const onClickButton = () => {
    ref.current.value = '';
  };

  return (
    <div>
      <input type="text" name="keyword" ref={ref} />
      <button onClick={onClickButton}>input 초기화</button>
    </div>
  );
};
```

## useLayoutEffect

> **useLayoutEffect**는 동기적으로 동작하며 paint하기 전에 실행된다. 화면에 그리기 전에 수행되므로 **useLayoutEffect**에 DOM에 영향을 미치는 코드를 넣어도 화면 깜빡임이 발생하지 않는다. 렌더링 이전에 하고 싶은 동작이나 렌더링할 상태가 Effect 내에서 초기화 하는 경우에 활용할 수 있다.
>
> 하지만 동기적인 동작에서 발생하는 단점을 가지고 있다. 만약에 위의 코드가 데이터를 불러오는 부분인데 10초가 걸린다고 가정하면 유저는 10초동안 빈 화면을 보게 되는 것이다.
>
> **useEffect**를 사용하여 설계하다가 뭔가 깜빡임에 문제가 있다면 **useLayoutEffect**를 사용하는것이 바람직하며, 공식문서에도 해당 상황에서는 **useLayoutEffect**를 권하고 있다.

## React StrictMode 란

> StrictMode는 애플리케이션 내의 잠재적인 문제를 알아내기 위한 도구입니다.

```jsx
import React from 'react';

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

### StricMode의 도움

- [안전하지 않은 생명주기를 사용하는 컴포넌트 발견](https://ko.legacy.reactjs.org/docs/strict-mode.html#identifying-unsafe-lifecycles)
- [레거시 문자열 ref 사용에 대한 경고](https://ko.legacy.reactjs.org/docs/strict-mode.html#warning-about-legacy-string-ref-api-usage)
- [권장되지 않는 findDOMNode 사용에 대한 경고](https://ko.legacy.reactjs.org/docs/strict-mode.html#warning-about-deprecated-finddomnode-usage)
- [예상치 못한 부작용 검사](https://ko.legacy.reactjs.org/docs/strict-mode.html#detecting-unexpected-side-effects)
- [레거시 context API 검사](https://ko.legacy.reactjs.org/docs/strict-mode.html#detecting-legacy-context-api)
- [Ensuring reusable state](https://ko.legacy.reactjs.org/docs/strict-mode.html#ensuring-reusable-state)
