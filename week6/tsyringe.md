# 6주차 TSyringe

## 학습 키워드

- TSyringe
- 의존성 주입(Dependency Injection)
- reflect-metadata
- sington (싱글톤)

## TSyringe

> **TSyringe**는 TypeScript용 DI 도구(IoC Container)로 External Store를 관리하는데 활용할 수 있다. React 컴포넌트 입장에서는 “전역”처럼 여겨진다. “Prop Drilling” 문제를 우아하게 해결할 수 있는 방법 중 하나(React로 한정하면 Context도 쓸 수 있다)이다.
>
- Typescript와 마찬가지로 MS에서 만들었다.
- JS/TS를 위한 경량 의존성 주입 컨테이너 이다.
- Tsyringe도 내부적으로는 context를 사용한다.

## 의존성 주입(Dependency Injection)

- 의존성 주입은 클래스간의 의존관계를 느슨하게 결합하는 디자인 패턴이다.
- 객체간의 의존성을 명시적으로 정의하고, 객체 생성/관리를 자동화해서 더 유연하게 프로그램을 만들 수 있다.

### 의존성 주입 장점

- 의존성이 줄어든다.
  - 의존한다는 것은 그 의존대상의 변화에 취약하다는 것이며, 즉 대상이 변화하였을 때, 이에 맞게 수정해야한다. DI로 구현하게 되었을 때, 주입받는 대상이 변하더라도 그 구현 자체를 수정할 일이 없거나 줄어들게된다
- 재사용성이 높은 코드가 된다.
- 테스트하기 좋은 코드가 된다.
- 가독성이 높아진다.

## reflect-metadata

- 타입스크립트에서 메타데이터를 활용하기 위해 필요한 라이브러리

### 사용 방법

```jsx
// install reflect-metadata library
npm i reflect-metadata --save

// add compiler option
tsc --target ES5 --emitDecoratorMetadata
```

```jsx
{
 "compilerOptions": {
  "target": "ES5",
  "experimentalDecorators": true,
  "emitDecoratorMetadata": true
 }
}
```

## Singleton Pattern

- 생성자가 여러개 호출 되어도 실제 생성은 한번만 생성되고 최초 생성된 객체만 계속 사용하는 디자인 패턴

### 사용 이유

- 공유 리소스 - 동일한 리소스를 공유해서 쓰는 경우
- 상태 유지 - 객체 상태가 유지되어야 하는 경우
- 제한된 인스턴스 생성 - 리소스를 절약하기 위해 인스턴스 생성 수를 제한
- 전역 접근 - 어디서든 접근가능하도록 하는 경우
