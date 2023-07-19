# Testing Library

## 학습 키워드

- Jest
- Describe-Context-It 패턴
- React Testing Library

## Jest

> **Jest**는 페이스북에서 만들어서 React와 더불어 많은 자바스크립트 개발자로 부터 좋은 반응을 얻고 있는 테스팅 라이브러리이다. 출시 초기에는 프런트앤드에서 주로 쓰였지만 최근에는 백앤드에서도 기존의 자바스크립트 테스팅 라이브러리를 대체하고 있다.

### 명령어

```bash
# 테스트 코드의 변화 실시간 반영
npx jest --watchAll

# 테스트 코드에 대한 자세한 설명
npx jext --verbose
```

## Describe-Context-It 패턴

```tsx
Describe에는 설명할 테스트 대상을 명시

describe('login', () => {

Context는 테스트 대상이 놓인 상황을 설명한다.
with 또는 when으로 시작하도록 한다.

context('with correct accountNumber and password ', () => {

It은 테스트 대상의 행동을 설명, 행동을 심플하게 설명

it('load accountNumber information', async () => {
```

## React Testing Library

> **React Testing Library**는 [Facebook에서 공식적으로 사용을 권장](https://ko.reactjs.org/docs/test-utils.html)하는 리액트 테스트 도구이다. 이 라이브러리는 **사용자가 컴포넌트를 사용하는 것**처럼 테스트를 작성할 수 있도록 설계되어있다.

> **React Testing Library**는 React 컴포넌트를 테스트하기 위해 설계된 라이브러리다.

### \***\*초기 세팅\*\***

```bash
React 프로젝트에 TypeScript 적용

$ npx create-react-app react-testing --template typescript

 or

$ yarn create react-app react-testing --template typescript
```

## **get**

- `getBy` 관련 쿼리는 원하는 요소를 찾지 못할 경우나 여러 개의 요소를 찾을 경우 에러를 던진다.
- `getAllBy` 관련 쿼리는 여러 요소를 찾아 배열을 반환한다. 원하는 요소를 찾지 못할 경우 에러를 던진다.
- 원소가 반드시 페이지에 존재해야만 하는 경우 활용할 수 있다.

## **find**

- `findBy` 관련 쿼리는 **원하는 원소가 없더라도 비동기적으로 기다리게 된다.**
- 여러 원소를 찾거나, 정해진 timeout동안 찾지 못하면 에러를 던진다.
- `findAllBy` 관련 쿼리는 여러 원소를 검색해 배열을 반환한다. 정해진 timeout동안 찾지 못하면 에러를 던진다.
- Promise를 리턴하며 실패 시 reject, 성공 시 resolve.
- **어떤 유저의 동작 후에 등장하는 원소 등을 테스트하고자 할 때 활용한다.**

## **query**

- queryBy 관련 쿼리는 getBy와 비슷하게 원소를 찾아 반환하나, 못 찾을 경우 에러를 던지지 않고 null을 반환한다. **여러 원소를 찾으면 에러를 던진다.**
- queryAllBy 관련 쿼리는 getAllBy와 비슷하게 여러 개의 원소를 찾아 배열로 반환하나, 하나도 찾지 못하면 에러 대신 빈 배열을 반환한다.
- 특정 요소를 찾을 수 없음을 assertion의 기준으로 둘 때 활용된다.

## **container**

- **container**는 컴포넌트를 렌더 한 결과를 감싸는 원소
- queryselector(), querySelectorAll()을 이용해 selector 문법으로 원소를 선택할 수 있다.

## **jest-dom**

- react-testing-library는 jest를 확장하여, 좀 더 쓰기 편한 assertion을 제공한다.
- toBeInTheDocument(), toHaveValue(), toBeDisabled(), toBeVisible() 등 DOM 테스팅에 특히 유용한 assertion 메서드를 제공한다.

### 예시

```jsx
it("뭔가 수행한다.", async () => {
  const { FirstNameInput, LastNameInput, clickIsOver21, FavoriteDrinkInput } =
    renderComplexForm();

  expect(FirstNameInput()).toBeInTheDocument();
  expect(LastNameInput()).toBeInTheDocument();

  await clickIsOver21();

  expect(FavoriteDrinkInput()).toBeInTheDocument();
});
```

### 결론

- 테스트가 소프트웨어가 사용되는 모습을 닮을수록, 테스트를 더욱 신뢰할 수 있게 된다.
  - The more your tests resemble the way your software is used, the more confidence they can give you.
  - 사용되는 모습이란? 사용자가 직접 앱을 사용하는 모습이다.
- React 컴포넌트의 특정 메서드나 상태를 테스트하는 게 아니라, 실제 유저가 사용하는 방식대로 테스트하는 접근하는 것이다.
- 유저가 페이지에서 어떤 DOM 요소에 접근하는 방법을 흉내 낸다.
- 이 방식으로 테스트 코드를 작성하면, 내부 구현이 바뀌어도 테스트가 깨지지 않는다.
- React 컴포넌트가 렌더링 한 결과에 대한 접근만 가능하다.
  - 결과 중심의 테스트
- 쿼리는 내부 상태나 내부 메서드에 접근할 수 없게 설계된다.
