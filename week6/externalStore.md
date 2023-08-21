# 6주차 External Store

## 학습 키워드

- 관심사의 분리
- Layered Architecture
- Flux Architecture
- useReducer
- useCallback

## 관심사의 분리(**Separation of Concerns)**

> 각각의 관심사에 따라 코드를 분리하는 기법
>
>
> 코드가 하나의 관심사만 신경쓰도록 분리하는 것
>

### 관심사의 분리 장점

- 특정한 변화에 대응하기 위해 읽고 이해하고 수정해야 하는 코드의 단위를 줄일 수 있어 유지 보수에 용이해진다.
- 하나의 코드가 하나의 기능을 담담하기에 여러 역할이 혼재된 코드보다 단위별로 재사용하기 쉬워진다.
- 코드의 기능 테스트 또한 쉬워진다.
- 관심사의 분리가 잘 된 소프트웨어는 낮은 결합도와 높은 응집도란 특징이 나타난다.
  - 낮은 결합도 (Loose Coupling) : 코드가 얽혀있지 않고 관심사에 따라 독립적으로 잘 분리되어 있다.
  - 높은 응집도 (High Cohesive) : 동일한 목적(관심사)를 가진 코드끼리 잘 모여있다.

## **계층화 아키텍처 (Layered Architecture)**

> **Layered Architecture**는 소프트웨어 개발에서 널리 사용되는 아키텍처로, 각 계층은 특정 역할과 관심사에 따라 구분되어 관심사의 분리를 통해 높은 유지보수성과 쉬운 테스트를 가능하게 한다.
>

양방향 데이터 흐름 때문에 복잡성이 생겼으므로 이를 단방향 데이터 흐름으로 만들어낸 아키텍쳐이다. 다음과 같은 구성원으로 이루어진다.

## Flux Architecture

- **액션 생성자(Action creator)**
  - 액션이란 어떤 행위인지와 그 행위로부터 넘겨받은 값들을 가진 하나의 객체를 말한다. 따라서 어떤 액션인지를 가리키는 `type` 과 넘겨받은 값인 `payload` 를 가진다. 액션 생성자는 기존 상태를 변경하기 위한 액션의 생성을 담당하며 해당 액션을 생성해서 디스패쳐에 넘겨준다.
- **디스패쳐(Dispatcher)**
  - 디스패쳐는 모든 액션들을 받아서 의존성을 적절히 처리해준 다음 모든 스토어에게 넘긴다. 여기서 중요한 점은 모든 스토어가 모든 액션을 받는다는 것이다.
- **스토어(Store)**
  - 스토어는 모든 액션을 받아서 자신에게 적합한 액션이 어떤 건지 필터링한다. 이후 상태값을 변경하고 자신에게 연결된 컨트롤러 뷰에게 상태가 변화되었음을 알린다.
- **컨트롤러 뷰(Controller View)와 뷰(View)**
  - 여기서 컨트롤러 뷰는 전체적으로 화면에 나타는 자식 뷰들과 스토어를 연결하는 매개체이다. 자식 뷰들은 컨트롤러 뷰에게 변화된 상태를 받고 그 상태에 따라 다시 렌더링이 된다.

## useReducer

> state를 관리하고 업데이트 하는 hook인 useState를 대체 할 수 있는 hook이다. 즉, useReducer는 useState 처럼 state를 관리하고 업데이트 할 수 있는 hook 이다.
>

```jsx
import React, { useReducer } from "react";
const [state, dispatch] = useReducer(reducer, initialState, init);
```

1. state
    - 컴포넌트에서 사용할 상태
2. dispatch 함수
    - 첫번째 인자인 reducer 함수를 실행시킨다.
    - 컴포넌트 내에서 state의 업데이트를 일으키키 위해 사용하는 함수
3. reducer 함수
    - 컴포넌트 외부에서 state를 업데이트 하는 함수
    - 현재state, action 객체를 인자로 받아, 기존의 state를 대체하여 새로운 state를 반환하는 함수
4. initialState
    - 초기 state
5. init
    - 초기 함수 (초기 state를 조금 지연해서 생성하기 위해 사용)

## useCallback

> **useCallback**은 useMemo와 비슷한 Hook이다. useMemo는 특정 결괏값을 재사용할 때 사용하는 반면, **useCallback**은 특정 함수를 새로 만들지 않고 재사용하고 싶을 때 사용하는 함수이다.
>

```jsx
const memoizedCallback = useCallback(function, deps);
```

**useCallback**은 첫 번째 인자로 넘어온 함수를, 두 번째 인자로 넘어온 배열 형태의 함수 실행 조건의 값이 변경될 때까지 저장해놓고 재사용할 수 있게 해 준다.

예를 들어 리액트 컴포넌트 안에 함수가 선언되어있을 때 이 함수는 해당 컴포넌트가 렌더링 될 때마다 새로운 함수가 생성되는데, **useCallback**을 사용하면 해당 컴포넌트가 렌더링 되더라도 그 함수가 의존하는 값(deps)들이 바뀌지 않는 한 기존 함수를 재사용할 수 있다.
