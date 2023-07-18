# 개발 환경 세팅

## 학습 키워드

- Node.js
- NPM(Node Package Manager)
  - package.json / package-lock.json
  - node_modules
  - npx
- ES Modules vs CommonJS

## Node.js

> **Node.js**는 확장성 있는 네트워크 애플리케이션(특히 서버 사이드) 개발에 사용되는 소프트웨어 플랫폼이다. 작성 언어로 [자바스크립트](https://ko.m.wikipedia.org/wiki/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8)를 활용하며 논블로킹(Non-blocking) I/O와 단일 스레드 이벤트 루프를 통한 높은 처리 성능을 가지고 있다.

## NPM(Node Package Manager)

> **npm**(노드 패키지 매니저/Node Package Manager)은 [자바스크립트](https://ko.m.wikipedia.org/wiki/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8) 프로그래밍 언어를 위한 [패키지 관리자](https://ko.m.wikipedia.org/wiki/%ED%8C%A8%ED%82%A4%EC%A7%80_%EA%B4%80%EB%A6%AC%EC%9E%90)이다. 자바스크립트 런타임 환경 [Node.js](https://ko.m.wikipedia.org/wiki/Node.js)의 기본 패키지 관리자이다.

## package.json

> **package.json**이란 현재 프로젝트에 관한 정보와 패키지 매니저(npm, yarn)을 통해 설치한 모듈들의 의존성을 관리하는 파일이다.

## package-lock.json

> **package-lock.json**은 npm이 node_lock 트리 또는 package.json을 수정하는 모든 작업에 대해 자동으로 생성된다. 생성된 정확한 트리를 설명하므로, 후속 설치에서 중간 종속성 업데이트에 관계없이 동일한 트리를 생성할 수 있습니다.

## node_modules

> **node_modules**는 package.json에 있는 모듈 뿐만 아니라, package.json에 있는 모듈이 의존하고 있는 모듈 전부를 포함하고 있다. 그래서 node_modules 디렉토리안에는 정말 많은 모듈들이 들어가 있다.

## npx

> **npx**는 npm 레지스트리에 있는 패키지를 더 쉽게 설치하고 관리하도록 도와주는 CLI(Command-line interface) 도구이다. npx는 npm을 더 편하게 사용하기 위해 탄생한만큼 npm을 통해 설치하는 모든 종류의 Node.js 기반의 파일을 간단하게 설치 및 실행할 수 있도록 도와준다

## Deno

> **Deno**는 V8 JavaScript 엔진 및 Rust 프로그래밍 언어를 기반으로하는 JavaScript 및 TypeScript 용 런타임이다.

## Fnm

> **Fnm**은 Fast Node Manager의 약어로 Node.js 버전 관리 도구 중 하나입니다. 빠르고 간단한 CLI 도구로, 다양한 Node.js 버전을 쉽게 설치하고 관리할 수 있다.

## ES Modules vs CommonJS

### CommonJS

- 파일 시스템에서 파일을 로드한다.
- 파일을 불러오는 동안 **주 스레드를 차단한다.**
- 그렇기에 파일 로드 - 구문 분석 - 인스턴스화 - 평가가 각 파일마다 바로 실행된다.
- 그렇기에 모듈 지정자에 변수를 넣을 수 있다.
- export 객체에 값을 **복사**해서 넣는다.

### ES Module

- entry 파일의 구문 분석 후 의존성(import)을 확인해서 해당 의존성 파일을 찾아서 다시 구문 분석을 반복한다.
- 파일을 불러오는 동안 **주 스레드를 차단하지 않는다.**
- 인스턴스화, 평가는 더 이상 구문 분석할 의존성이 발견되지 않으면 실행한다
- 그렇기에 모듈 지정자에 변수를 넣을 수 없다(다만 동적 import를 쓰면 가능)
- export는 **참조**를 반환하는 함수를 정의한다.
- 동적 import는 별개의 entry 파일로 취급되어 새로운 그래프를 만든다.

### ES Module와 CommonJS 차이에 따른 결과

- export하는 파일에서 비동기 처리로 값이 바뀐다면, CommonsJS에서는 반영이 되지 않지만 ESM은 반영 될 수 있다(비동기로 다시 호출한다면).
- 순환 참조의 경우 CommonJS는 빈 객체를, ESM은 RefernceError를 발생시킨다.
