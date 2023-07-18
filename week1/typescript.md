# TypeScript

## 학습 키워드

- REPL
- TypeScript
  - Interface vs Type
  - 타입 추론
  - Union Type vs Intersection Type
  - Optional Parameter

## REPL

> **REPL**은 Read-Eval-Print-Loop의 약자로 애플리케이션 실행 상태에서 사용자가 입력한 명령어(소스코드)를 읽고(Read) 명령어를 평가(Eval)하고 결과를 출력(Print)한 다음 다시 입력을 기다리는 상태로 돌아가는 과정을 반복(Loop)을 의미한다.

> **REPL**은 주로 개발자들이 소스 코드 실행 결과를 빨리 확인해야 하는 경우 사용한다.

## TypeScript

> 타입스크립트는 자바스크립트에 타입을 부여한 언어다. 자바스크립트의 확장된 언어라고 볼 수 있다. 타입스크립트는 자바스크립트와 달리 브라우저에서 실행하려면 파일을 한번 변환해주어야 한다. 이 변환 과정을 우리는 **컴파일(complile)** 이라고 부른다.

```tsx
- 타입 별칭 `type sn = number | string;`
- 인터페이스 `interface I { x: number[]; }`
- 클래스 `class C { }`
- 이넘 `enum E { A, B, C }`
- 타입을 가리키는 `import` 구문
```

## Interface vs Type

> 타입 별칭과 인터페이스는 매우 유사하며, 대부분의 경우 둘 중 하나를 자유롭게 선택하여 사용할 수 있다. `interface`가 가지는 대부분의 기능은 `type`에서도 동일하게 사용 가능하다. 이 둘의 가장 핵심적인 차이는, 타입은 새 프로퍼티를 추가하도록 개방될 수 없는 반면, 인터페이스의 경우 항상 확장될 수 있다는 점이다.

```tsx
인터페이스 확장

interface Animal {
  name: string
}

interface Bear extends Animal {
  honey: boolean
}

const bear = getBear()
bear.name
bear.honey

Type을 통하여 타입 확장

type Animal = {
  name: string
}

type Bear = Animal & {
  honey: Boolean
}

const bear = getBear();
bear.name;
bear.honey;
```

```tsx
기존의 인터페이스에 새 필드를 추가

interface Window {
  title: string
}

interface Window {
  ts: TypeScriptAPI
}

const src = 'const a = "Hello World"';
window.ts.transpileModule(src, {});

타입은 생성된 뒤에는 달라질 수 없다

type Window = {
  title: string
}

type Window = {
  ts: TypeScriptAPI
}

 // Error: Duplicate identifier 'Window'.
```

- 확장하기Interface 확장하기 `extends`Type 교집합을 통하여 타입 확장하기 `&`
  - 인터페이스에 새 필드를 추가할 수 있고 타입은 생성한 뒤에는 달라질 수 없다.
  - 인터페이스는 오직 객체의 모양을 선언하는 데에만 사용되며, 기존의 원시 타입에 별칭을 부여하는 데에는 사용할 수는 없다.
- **개인적 선호**에 따라 인터페이스와 타입 중에서 선택할 수 있으며, 필요하다면 **TypeScript가 다른 선택을 제안**할 것이다. 잘 모르겠다면, **우선 interface를 사용하고 이후 문제가 발생하였을 때 type을 사용하자.**

## \***\*타입 추론(Type Inference)\*\***

> 타입 추론이란 타입스크립트가 코드를 해석해 나가는 동작을 의미한다.

[타입 추론 | 타입스크립트 핸드북](https://joshua1988.github.io/ts/guide/type-inference.html#타입-추론-type-inference)

## Union Type vs Intersection Type

> 유니언은 타입이 여러 타입 중 하나일 수 있음을 선언하는 방법이다. 예를 들어, `boolean` 타입을 `true` 또는 `false`로 설명할 수 있다.

```tsx
1. type MyBool = true | false;

2. type WindowStates = "open" | "closed" | "minimized";

3. type OddNumbersUnderTen = 1 | 3 | 5 | 7 | 9;

// 유니언은 다양한 타입을 처리하는 방법을 제공하는데,
// 예를 들어 array 또는 string을 받는 함수가 있을 수 있다.

function getLength(obj: string | string[]) {
  return obj.length;
}
```

## Optional Parameter

> 함수내에 인자를 전달 하지 않아도 주어진 함수의 기능을 수행하게 하기위해 인자에 따로 옵션을 부여하는 방식

```tsx
//파라미터 이름 뒤에 ?를 붙이면
//인수가 전달되지 않더라도 함수의 기능을 수행한다

function 함수이름(파라미터1: 타입, 파라미터2?: 타입): 반환타입 {
  //함수 기능...
}
```

## 라이브러리에 ts 파일이 없는 경우 참고(d.ts 파일 제공)

[https://github.com/DefinitelyTyped/DefinitelyTyped](https://github.com/DefinitelyTyped/DefinitelyTyped)
