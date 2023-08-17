# 4주차 Fetch API & CORS

## 학습 키워드

- Fetch API 란
- Promise
- ReadableStream
- Unicode
- CORS 란

## Fetch API 란

> **Fetch API**는 HTTP 파이프라인을 구성하는 요청과 응답 등의 요소를 JavaScript에서 접근하고 조작할 수 있는 인터페이스를 제공하며 서버로 네트워크 요청을 보내고 응답을 받을 수 있도록 해준다.

```jsx
// 예1
async function logJSONData() {
  const response = await fetch('http://example.com/movies.json');
  const jsonData = await response.json();
  console.log(jsonData);
}

// 예2
fetch(url)
  .then((res) => {
    console.log(res);
  })
  .catch((error) => {
    console.log(error);
  });
```

## **Promise**

> **Promise**는 자바스크립트 비동기 처리에 사용되는 객체이다. 여기서 자바스크립트의 비동기 처리란 ‘특정 코드의 실행이 완료될 때까지 기다리지 않고 다음 코드를 먼저 수행하는 자바스크립트의 특성’을 의미한다.

### **프로미스의 3가지 상태(states)**

> 프로미스를 사용할 때 알아야 하는 가장 기본적인 개념이 바로 프로미스의 상태(states)이다. 여기서 말하는 상태란 프로미스의 처리 과정을 의미한다. `new Promise()`로 프로미스를 생성하고 종료될 때까지 3가지 상태를 갖는다.

- Pending(대기) : 비동기 처리 로직이 아직 완료되지 않은 상태
- Fulfilled(이행) : 비동기 처리가 완료되어 프로미스가 결과 값을 반환해준 상태
- Rejected(실패) : 비동기 처리가 실패하거나 오류가 발생한 상태

```jsx
//Pending(대기)
new Promise();

new Promise(function(resolve, reject) {
 // ...
}

//Fulfilled(이행)
function getData() {
  return new Promise(function(resolve, reject) {
    var data = 100;
    resolve(data);
  });
}

// resolve()의 결과 값 data를 resolvedData로 받는다.
getData().then(function(resolvedData) {
  console.log(resolvedData); // 100
});

//Rejected(실패)
function getData() {
  return new Promise(function(resolve, reject) {
    reject(new Error("Request is failed"));
  });
}

// reject()의 결과 값 Error를 err에 받는다.
getData().then().catch(function(err) {
  console.log(err); // Error: Request is failed
});
```

## **ReadableStream**

> Streams API의 **ReadableStream** 인터페이스는 바이트 데이터를 읽을수 있는 스트림을 제공해준다.

## Unicode

> **Unicode**는 전세계에서 사용하는 모든 문자들을 하나의 문자 셋으로 표현하는 문자표이다.
>
> 멀티바이트에서 발생하는 호환성들의 문제를 해결하기 위해 만들어진 표준코드이며,
>
> 아스키코드로 표현할 수 없는 문자들을 표현할 수 있고, 글자와 숫자 즉 키와 값이 1대1로 매칭된다.

## **CORS(Cross-Origin Resource Sharing)**

> **다른 출처의 자원을** 공유. 교차 출처 리소스 공유 (Cross-origin Resource Sharing, Cors)는 추가 HTTP헤더를 사용하여, 한 출처에서 실행 중인 웹 애플리케이션이 다른 출처의 선택한 자원에 접근할 수 있는 권한을부여하도록 **브라우저에** 알려주는 체제이다.

서버가 웹 브라우저에서 리소스를 로드할 때 다른 오리진을 통해 로드하지 못하게 하는 HTTP 헤더 기반 메커니즘이다.

>

### 필요한 이유

> CORS가 없이 모든 곳에서 데이터를 요청할 수 있게 된다면, 다른 사이트에서 원래 사이트를 흉내낼 수 있게 된다. 만약 기존 사이트와 완전히 동일하게 동작하도록 하여 사용자가 로그인을 하도록 하고, 로그인했던 세션 또는 토큰을 탈취하여 악의적으로 정보를 꺼내오거나 다른 사용자의 정보를 입력하는 등 헤킹을 할 수 있다. 하지만 이런 공격을 할 수 없도록 브라우저에서 보호하고, 필요한 경우에만 서버와 협의하여 요청할 수 있도록 하기 위해서 필요한 것이다.

Express에서는 패키지 설치하여 사용하면 된다.

```bash
npm i cors
npm i -D @types/cors
```

```jsx
import express from 'express';
import cors from 'cors';

const app = express();

app.use(cors());
```
