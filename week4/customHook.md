# 4주차 useRef & Custom Hook

## 학습 키워드

- useRef
- Hook의 규칙

## useRef

> **useRef**는 .current 프로퍼티로 전달된 인자(initialValue)로 초기화된 **변경 가능한 ref 객체**를 반환하며, **저장공간 또는 DOM요소에 접근하기 위해 사용되는 React Hook**이다. 여기서 Ref는 reference, 즉 참조를 뜻한다.
>
> 자바스크립트를 사용 할 때 보통 특정 DOM 을 선택하기 위해서 querySelector 등의 함수를 사용한다.
>
> React를 사용하는 프로젝트에서도 가끔씩 DOM 을 직접 선택해야 하는 상황이 필요하다. 그럴때 useRef라는 React Hook을 사용하면 된다.

## Custom Hook

> **custom hook**으로 반복되는 훅 활용 메소드들을 하나로 줄여줌으로써 더 간결하고 보기 좋은 코드를 만들 수 있으며, 이름이 ”use“로 시작하고, 안에서 다른 Hook을 호출한다면 그 함수를 custom Hook이라고 부를 수 있다.

### hook 규칙

- 최상위에서만 Hook을 호출
  - 반복문, 조건문, 중첩된 함수에서 Hook 호출하면 안된다.
  - 조건문을 Hook내부에 사용하는 것은 가능(useEffect)하다.
  - 이 규칙을 따라야 동일한 순서로 Hook 호출되는 것이 보장된다.
- React 함수 내에서만 Hook을 호출
  - JavaScript 내에서 호출하지 않아야한다.
- 규칙을 지켜야하는 이유
  - 모든 상태 관련 로직을 소스코드에서 명확하게 보이도록 할 수 있다.
