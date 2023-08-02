# 3주차(React State)

## 학습 키워드

- React state란?
- DRY 원칙
- SSOT(Single Source of Truth)
- useState
- 1급 객체(first-class object)란?
- Lifting State Up

## React state란?

> **state**란 리액트에서 이벤트에 의해 변경되는 동적인 값이다.
>
> 버튼을 클릭하는 onClick 이벤트, input 입력으로 인해 발생하는 onChange 이벤트에 의해 입력값이 변경된 경우 사용 많이 사용된다. props는 부모 컴포넌트가 설정하는 값이며 읽기 전용이지만, state는 하위 컴포넌트도 데이터를 변경할 수 있다. 함수형 컴포넌트는 '**useState**'라는 **Hook** 을 사용하여 **state**를 다룰 수 있다.

## DRY 원칙

> Do not Repeat Yourself(반복하지마라)
> 모든 형태의 정보 중복을 지양하는 원리이다. 특히 다층 구조 시스템에서 유용하다.
>
> 중복배제 원리는 한마디로 “모든 지식은 시스템 내에서 유일하고 중복이 없으며
>
> 권위있는 표상만을 가진다”는 말로 기술할 수 있다.

## 단일 진실 공급원(SSOT)

> 단일 진실 공급원(SSOT)은 정보 시스템 설계 및 이론 중 하나로 **정보와 스키마를 오직 하나의 출처에서만 생성, 편집하도록 하는 방법론**이다. **단일 출처를 통해 데이터를 생성, 편집, 접근하므로 데이터의 정합성을 지키고 잘못된 데이터 유통을 방지하고 모두가 동일한 데이터를 참고하게 하고 있다.**

## useState

> 반드시 setState 로 데이터를 변경해야한다.
> \*\*\*\*state 값을 변경할 때는 반드시 setState를 사용하여 변경해야 한다.
> setState를 사용한 경우, state값이 변경되면 useState가 변경을 감지하고, 자식 컴포넌트들까지 리렌더링이 발생한다.
> 직접 state를 수정하게 되면 리액트가 render 함수를 호출하지 않아 변경이 일어나도 렌더링이 일어나지 않을 수 있다.

```jsx
// useState

const [state, setState] = useState(initialState);
const [상태, 세터함수] = useState(초기값);
```

## 1급 객체(first-class object)

> **일급객체(First-class Object)**란 다른 객체들에 일반적으로 적용 가능한 연산을 모두 지원하는 객체를 가리킨다.
>
> - 변수에 할당(assignment)할 수 있다.
> - 다른 함수를 인자(argument)로 전달 받는다.
> - 다른 함수의 결과로서 리턴될 수 있다.

## Lifting State Up

> 종종 동일한 데이터에 대한 변경사항을 여러 컴포넌트에 반영해야 할 필요가 있다. 이럴 때는 가장 가까운 공통 부모 컴포넌트로 state를 끌어올리는 것이 좋다.
