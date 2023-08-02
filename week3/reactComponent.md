# React Component

## 학습 키워드

- REST API 와 GraphQL
  - REST API 란 무엇인가
  - GraphQL은 왜 등장했는가?
  - REST API vs GraphQL
- JSON
- DSL(Domain-Specific Language)
- 선언형 프로그래밍
- 명령형 프로그래밍
- SRP(단일 책임 원칙)
- Atomic Design
- React component 와 props

## Thinking in React

### Step 1

> Break the UI into a component hierarchy.
> UI 요소를 component 단위로 쪼개기

### Step 2

> Build a static version in React.
> 상호작용이 없는(static한) React page 만들기

## REST API 와 GraphQL

### REST API 란 무엇인가

> REST의 원리를 따르는 API를 **REST API**라고 한다.

### **REST API 설계 규칙**

1. URI는 동사보다는 명사를, 대문자보다는 소문자를 사용하여야 한다.
2. 마지막에 슬래시 (/)를 포함하지 않는다.
3. 언더바 대신 하이폰을 사용한다.
4. 파일확장자는 URI에 포함하지 않는다.
5. 행위를 포함하지 않는다.

### RESTful이란?

> **RESTFUL**이란 REST의 원리를 따르는 시스템을 의미한다. 하지만 REST를 사용했다 하여 모두가 RESTful 한 것은 아니다.  REST API의 설계 규칙을 올바르게 지킨 시스템을 RESTful하다 말할 수 있으며, 모든 CRUD 기능을 POST로 처리 하는 API 혹은 URI 규칙을 올바르게 지키지 않은 API는 REST API의 설계 규칙을 올바르게 지키지 못한 시스템은 REST API를 사용하였지만 RESTful 하지 못한 시스템이라고 할 수 있다.

### GraphQL이란?

> **GraphQL** 은 한 문장으로 얘기하자면 **페이스북에서 만든 API 를 위한 쿼리 언어** 라고 할 수 있다.
> **GraphQL** 은 **웹 클라이언트가 데이터를 서버로부터 효율적으로 가져오는 것이 목적**인 쿼리 언어이다.

### SQL (Structed Query Language)

> **SQL** 은 **데이터베이스 시스템에 저장된 데이터를 효율적으로 가져오는 것이 목적**인 쿼리 언어이다.

### GraphQL은 왜 등장했는가?

> RESTful API 로는 다양한 기종에서 필요한 정보들을 일일히 구현하는 것이 힘들었다.
> 예로, iOS 와 Android 에서 필요한 정보들이 조금씩 달랐고, 그 다른 부분마다 API 를 구현하는 것이 힘들었다.
> 이 때문에 정보를 사용하는 측에서 원하는 대로 정보를 가져올 수 있고, 보다 편하게 정보를 수정할 수 있도록 하는 표준화된 Query language 를 만들게 되었다.

### REST API vs GraphQL

1. GraphQL API 는 주로 하나의 Endpoint 를 사용한다.
2. GraphQL API 는 요청할 때 사용한 Query 문에 따라 응답의 구조가 달라진다.

## JSON (JavaScript Object Notation)

- JavaScript Object Notation라는 의미의 축약어로 데이터를 저장하거나 전송할 때 많이 사용되는 **경량의 DATA 교환 형식**
- Javascript에서 객체를 만들 때 사용하는 표현식을 의미한다.
- JSON 표현식은 사람과 기계 모두 이해하기 쉬우며 용량이 작아서, 최근에는 JSON이 XML을 대체해서 데이터 전송 등에 많이 사용한다.
- JSON은 데이터 포맷일 뿐이며 어떠한 통신 방법도, 프로그래밍 문법도 아닌 단순히 데이터를 표시하는 표현 방법일 뿐이다.

## JSON 특징

- 서버와 클라이언트 간의 교류에서 일반적으로 많이 사용된다.
- 자바스크립트 객체 표기법과 아주 유사하다.
- 자바스크립트를 이용하여 JSON 형식의 문서를 쉽게 자바스크립트 객체로 변환할 수 있는 이점이 있다.
- **JSON 문서 형식은 자바스크립트 객체의 형식을 기반으로 만들어졌다.**
- 자바스크립트의 문법과 굉장히 유사하지만 **텍스트 형식일 뿐**이다.
- 다른 프로그래밍 언어를 이용해서도 쉽게 만들 수 있다.
- 특정 언어에 종속되지 않으며, 대부분의 프로그래밍 언어에서 JSON 포맷의 데이터를 핸들링 할 수 있는 라이브러리를 제공한다.

## DSL(Domain-Specific Language)

> 특정 도메인(산업, 분야등 특정 영역)에 특화된 언어를 말한다.

### **DSL의 장점과 단점**

**장점**

- 반복이 제거되고 비슷한 처리 코드는 자동 생성(템플릿) 된다.
- 프로그래밍 코드의 양이 적고 가독성이 높다.
- 특정 프로그래머(lay programer - martin fowler)들과 커뮤니케이션이 쉽다.

. XML, CSS, SQL 등

**단점**

- 설계가 어렵다.
- 잘 설계가 되지 않는다면 읽기 어려운 코드가 될 수 있다.
- 하위 호환성을 유지해야 한다.

**우리 주변에 있는 DSL**

- java

. ANT, Maven, struts-config.xml, Seasar2 S2DAO, HQL(Hibernate Query Language), JMock

- Ruby

. Rails Validations, Rails ActiveRecord, Rake, RSpec, Capistrano, Cucumber

- 기타

. SQL, CSS, Regular Expression(정규식), Make, graphviz

## [선언형 프로그래밍](https://ko.wikipedia.org/wiki/%EC%84%A0%EC%96%B8%ED%98%95_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)

> 프로그램이 어떤 방법으로 해야 하는지를 나타내기보다 무엇과 같은지를 설명하는 경우에 "선언형"이라고 한다.

## [명령형 프로그래밍](https://ko.wikipedia.org/wiki/%EB%AA%85%EB%A0%B9%ED%98%95_%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D)

> **명령형 프로그래밍**은 선언형 프로그래밍과 반대되는 개념으로, 프로그래밍의 상태와 상태를 변경시키는 구문의 관점에서 연산을 설명하는 프로그래밍 패러다임의 일종이다. 자연 언어에서의 명령법이 어떤 동작을 할 것인지를 명령으로 표현하듯이, 명령형 프로그램은 컴퓨터가 수행할 명령들을 순서대로 써 놓은 것이다.

## SRP(단일 책임 원칙)

> **단일 책임 원칙(SRP)**는 **객체는 단 하나의 책임만 가져야 한다는 원칙**을 말한다. 여기서 '책임' 이라는 의미는 하나의 '기능 담당'으로 보면 된다. 즉, 하나의 클래스는 하나의 기능 담당하여 하나의 책임을 수행하는데 집중되어야 있어야 한다는 의미이다.

## Atomic Design

> **Atomic Design**은 최근 React를 이용하여 컴포넌트 개발할 때 떠오르고 있는 디자인 기법 중 하나로 **효율적인 인터페이스 디자인 시스템을 만들어내기 위해 사용**된다.

**Atomic Design**은 다음과 같이 크게 5가지로 구성된다.

- Atom (원자)
- Molecule (분자)
- Organism (유기체)
- Template (템플릿)
- Page (페이지)

## React component 와 props

### React component

> 리액트로 만들어진 앱을 이루는 최소한의 단위

**함수형 컴포넌트 (Stateless Functional Component)**

- 가장 간단하게 컴포넌트를 정의하는 방법은 자바스크립트 함수를 작성하는 것이다.

```jsx
import React from "react";

function MyComponent(props) {
  return <div>Hello, {props.name}</div>;
}

export default MyComponent; //다른 JS파일에서 불러올 수 있도록 내보내주기
```

**클래스형 컴포넌트 ( Class Component )**

```jsx
import React from "react";

class MyComponent extends React.Component {
  constructor(props) {
    // 생성함수
    super(props);
  }

  componentDidMount() {
    // 상속받은 생명주기 함수
  }

  render() {
    // 상속받은 화면 출력 함수, 클래스형 컴포넌트는 render() 필수
    return <div>Hello, {this.props.name}</div>;
  }
}

export default MyComponent; //다른 JS파일에서 불러올 수 있도록 내보내주기
```

### props

> 프로퍼티, props(properties의 줄임말) 라고 한다.
>
> 상위 컴포넌트가 하위 컴포넌트에 값을 전달할때 사용한다.(단방향 데이터 흐름 갖는다.)
>
> 프로퍼티는 수정할 수 없다는 특징이 있다.(자식입장에선 읽기 전용인 데이터이다.)

```jsx
// App.js

import React, { Component } from "react";
import Header from "./component/Header";
import Footer from "./component/Footer";
import Main from "./component/Main";

function App() {
  return (
    <div>
      <Header />
      <Main name="함우성" />
      <Footer />
    </div>
  );
}

export default App;
```

```jsx
// Main.js

import React from "react";

function Main(props) {
  return (
    <div>
      <main>
        <h1>안녕하세요. {props.name} 입니다.</h1>
      </main>
    </div>
  );
}

export default Main;
```
