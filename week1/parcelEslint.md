# Parcel & ESLint

## 학습 키워드

- Bundler(번들러)
  - Parcel
- Lint(린트)
  - ESLint

## Bundler(번들러)

> **Bundler(번들러)**는 의존성이 있는 모듈 코드를 하나(또는 여러 개)의 파일로 만들어주는 도구이다.

> **Bundler(번들러)**란 dependency가 있는 자바스크립트 파일들을 최적화, 압축하여 하나 혹은 여러개의 static 파일로 빌드해주는 컴파일러이다.

> 브라우저 환경에서는 CommonJS나 일부 ES6 Module로 작성된 코드(크롬과 같은 최신 브라우저에서는 ES6 Module을 지원한다)는 바로 실행할 수가 없으므로 모듈 코드를 분석하고 자바스크립트 모듈 스펙에 따라 새로운 코드로 가공이 필요하다.

### 기능

- 자주 사용 되는 코드를 별도의 파일로 만들어서 필요할 때마다 재활용할 수 있다.
- 코드를 개선하면 이를 사용하고 있는 모든 애플리케이션의 동작이 개선된다.
- 코드 수정 시에 필요한 로직을 빠르게 찾을 수 있다.
- 필요한 로직만을 로드해서 메모리의 낭비를 줄일 수 있다.
- 한번 다운로드된 모듈은 웹브라우저에 의해서 저장되기 때문에 동일한 - 로직을 로드 할 때 시간과 네트워크 트래픽을 절약 할 수 있다. (브라우저에서만 해당)

### Parcel

> **Parel**은 Webpack과 함께 bundler 시장의 점유율을 나눠갖고 있는 **모듈 번들러**이다.

```bash
npm install --save-dev parcel-bundler
```

## Lint(린트)

> 에러가 있는 코드에 표시를 달아주는 것을 뜻하며, 에러와 코딩 스타일을 잡아주기 때문에 여러 명이 코드를 작성하더라도 한 사람이 코딩한 것처럼 깔끔하게 만들어줄 수 있다.

> 잡아내고 싶은 에러의 기준은 직접 설정할 수 있으며, 문법적인 오류만 잡아낼 수도 있고 세미콜론(";") 사용과 같은 전반적인 코딩 스타일을 정해둘 수도 있다.

### ESLint

> 자바스크립트 코드를 검사하기 위해 개발된 Lint 도구이다.

```bash
# 문제 수정
npm run lint

# 문제 알림
npx eslint --ext .tsx .
```

### 설정

```bash
.vscode 폴더 생성
mkdir .vscode

settings.json 파일 생성
touce settings.json
```

```json
settings.json
{
  "editor.rulers": [80], //80열에서 줄 긋기
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "trailing-spaces.trimOnSave": true //save하면 끝에 있는 줄 삭제
}

```
