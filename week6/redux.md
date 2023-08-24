# 6주차 Redux

## Redux

> **Redux**는 리액트 없이도 사용할 수 있는 상태관리(state management) JavaScript 라이브러리이다.
애플리케이션의 많은 부분에 필요한 "전역" 상태를 관리하는 데 도움이 된다.
>

### Action

- 어떤 동작을 할것인가, 객체형태로 정의를한다. 이때 `type` 을 필수로 사용한다.
- 어떤 동작을 하는지 명시해주는 역할을 하기 때문이며, 대문자와 Snake Case로 작성한다. 여기에 필요에 따라 payload 를 작성해 구체적인 값을 전달한다.

### Dispatch

- Dispatch는 Reducer로 Action을 전달해주는 함수이다. Dispatch의 전달인자로 Action 객체가 전달된다.
- Action 객체를 전달받은 Dispatch 함수는 Reducer를 호출한다.

### Reducer

- Reducer는 Dispatch에게서 전달받은 Action 객체의 type 값에 따라서 상태를 변경시키는 함수이다.
- Reducer는 순수함수여야 한다.외부 요인으로 인해 기대한 값이 아닌 엉뚱한 값으로 상태가 변경되는 일이 없어야하기 때문이다.

### Store

- Store는 상태가 관리되는 단 하나의 저장소의 역할을 한다. (Redux 앱의 state가 저장되어 있는 공간) 아래 코드와 같이 createStore 메서드를 활용해 Reducer를 연결해서 Store를 생성할 수 있다.

### useSelector()

- 컴포넌트와 state를 연결하여 Redux의 state에 접근할 수 있게 해주는 메서드이다.

### useDispatch()

- Action 객체를 Reducer로 전달해 주는 메서드이다.

### 🗣 3가지 원칙

`Single source of truth`

- 동일한 데이터는 항상 같은 곳에서 가지고 와야 한다는 의미로, Redux에는 데이터를 저장하는 Store라는 단 하나뿐인 공간이 있음과 연결이 되는 원칙이다.

`State is read-only`

- 상태는 읽기 전용이라는 뜻으로, React에서 상태갱신함수로만(set) 상태를 변경할 수 있었던 것처럼, Redux의 상태도 직접 변경할 수 없다. 즉,Action 객체가 있어야만 상태를 변경할 수 있음과 연결되는 원칙이다.

`Changes are made with pure functions`

- 변경은 순수함수로만 가능하다는 뜻으로, 상태가 엉뚱한 값으로 변경되는 일이 없도록 순수함수로 작성되어야하는 Reducer와 연결되는 원칙이다.
