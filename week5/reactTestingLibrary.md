# 5주차 React Testing Library

## 학습 키워드

- React Testing Library
- given - when - then 패턴
- Mocking
- Test fixture

## React Testing Library

> React Testing Library는 [Facebook에서 공식적으로 사용을 권장](https://ko.reactjs.org/docs/test-utils.html)하는 리액트 테스트 도구이다. 이 라이브러리는 **사용자가 컴포넌트를 사용하는 것**처럼 테스트를 작성할 수 있도록 설계되어있다.

### 장점

- 빠르게 작동
- 테스트 시나리오 작성이 쉬움

### 예시

```jsx
//src/components/Counter.tsx

import React, { ReactElement } from 'react';

interface CounterProps {
  count: number;
  onIncrease: () => void;
  onDecrease: () => void;
}

function Counter({
  count,
  onDecrease,
  onIncrease,
}: CounterProps): ReactElement {
  return (
    <div>
      <h1>Counter</h1>
      <button onClick={onIncrease}>증가</button>
      <h3>{count}</h3>
      <button onClick={onDecrease}>감소</button>
    </div>
  );
}

export default Counter;
```

```jsx
//src/App.tsx
import React, { useState } from 'react';
import Counter from './components/Counter';

function App() {
  const [count, setCount] = useState(0);

  const onIncrease = () => setCount(count + 1);
  const onDecrease = () => setCount(count - 1);

  return (
    <div>
      <Counter count={count} onDecrease={onDecrease} onIncrease={onIncrease} />
    </div>
  );
}

export default App;
```

```jsx
//src/components/__test__/Counter.test.tsx
import { render } from '@testing-library/react';

const CounterProps = {
  count: 0,
  onIncrease: jest.fn(),
  onDecrease: jest.fn(),
};

describe('<Counter />', () => {});
```

<aside>
💡 CounterProps는 Counter 컴포넌트에 넣어줄 props들이다. 여기서 jest.fn()은 실제 함수를 넣어주는 것이 아닌 가짜 함수를 넣어주는 것이다.

여기서 가짜 함수를 넣어주는 이유는 React-testing-library로 함수의 로직을 테스트 하는 것이 아닌, 사용자 관점에서 컴포넌트가 동작하는지를 보기 위한 것이기 때문에, 로직이 없는 가짜 함수를 넣어줘도 상관없기 때문이다.

</aside>

## given - when - then 패턴

### \***\*Given(준비)\*\***

> 시나리오 진행에 필요한 값을 설정, 테스트의 상태를 설정
> 시나리오에서 필요한 값을 미리 추출하여 선언한다. 이 데이터들은 테스트의 전제 조건이다.

### \***\*When(실행)\*\***

> 시나리오 진행 필요조건 명시, 테스트하고자 하는 행동
> 지정한 동작(행동)을 의미한다.

### \***\*Then(검증)\*\***

> 시나리오를 완료했을 때 보장해야 하는 결과를 명시, 예상되는 변화 설명
> 지정한 동작(행동)으로 인해 예쌍되는 변화에 대해 설명한다.

```jsx
// given
const a = 1;
const b = 2;

// when
const result = plus(a,b);

// then
assert result === 3;
```

```jsx
describe('계산 테스트', () => {
  test('0 값을 받았을때 1값을 반환한다.', () => {
    // given
    const calculator = new Calculator();
    const value = 0;
    // when
    const result = calculator.increment(value);
    // then
    expect(1).toBe(result);
  });
});
```

## Mocking

> **mocking**은 실행을 위해 특정 컴포넌트가 필요하면, 해당 컴포넌트를 mock이라는 가짜 컴포넌트로 교체하는 기술을 의미한다. 예를 들어 `단일 서비스` 테스트를 위하여 `axios` 호출이 필요하면, 실제로 axios를 호출하는게 아니라 `axios`와 인터페이스가 똑같은 `mock`을 만들어 주입해줍니다. 혹은 함수 단위로 mocking을 할 수있다.

**최근에는 API 라이브러리를 교체나 추상화를 염두해두고 Mock Api 서버를 사용해서 Mock을 만들기도 한다.**

>

### **jest.fn()**

변수에 할당하여 가짜 함수를 생성하는 함수다. 인자로 가짜 함수가 실행할 함수를 넣을 수 있다. 아무것도 넣지 않으면 undefined를 반환한다.

```jsx
const mockFn = jest.fn(); // mockFn은 빈 함수

mockFn(1); // undefined

const mockFn = jest.fn((name) => `My name is ${name}`);

console.log(mockFn('John')); // 'My name is John'
```

jest.fn()로 만들어진 가짜 함수의 반환값이나 함수 자체 등을 조작할 수 있는 여러 메서드들이 있으니 필요시 찾아서 사용 가능하다.

### **jest.mock()**

모듈에 있는 함수들을 한꺼번에 Mocking할 때 사용할 수 있다. 가져온 함수들은 이름만 빌려와 가짜 함수를 만드는거고 기능은 복제해오지 않는다.

첫번째 인수는 모듈의 경로, 두번째 인수는 해당 모듈을 대체할 가짜 모듈을 생성하는 함수를 전달한다.

```jsx
export function add(a, b) {
  return a + b;
}

export function subtract(a, b) {
  return a - b;
}
```

```jsx
import { add, subtract } from './math';

jest.mock('./math', () => ({
  add: jest.fn(),
  subtract: jest.fn(),
}));

test('add function is called', () => {
  add(1, 2);
  expect(add).toHaveBeenCalledWith(1, 2);
});
```

### 초기화

> `가짜함수명.mockClear()` 와 `jest.clearAllMocks()` 등이 있으며, 해당 함수들은 보통 `before` 또는 `after` 함수 내에서 사용된다.

## Test fixture

> 중복 발생되는 무언가(행위)를 고정시켜 한곳에 관리하도록 하겠다는 개념
> 소프트웨어를 일관되게 테스트하기 위해 중복되는 부분을 한 곳에 몰아서 사용

### 장점

- 각 테스트가 항상 동일한 설정으로 시작하기 때문에 테스트를 반복할 수 있다.
- 메소드를 다른 함수로 분리하고 각 기능을 다른 테스트에 재사용할 수 있다.
- 테스트 코드 설계가 용이함이전 테스트 실행에서 남은 항목으로 작업하는 대신, 알려진 초기 상태로 테스트를 미리 구성할 수 있다.
