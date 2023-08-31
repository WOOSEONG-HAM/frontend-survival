# 7주차 Routing

## 학습 키워드

- HTML DOM API
    - Location
    - pathname

## HTML DOM API

> DOM API(**D**ocument **O**bject **M**odel **A**pplication **P**rogramming **I**nterface)의 약어이다.
흔히 우리가 **HTML에서 제어**하는 div, span, input 등의 **요소들을 Document Object Model** 이라하며, 프로그램을 사용하기 위한 **명령들의 집합을 Application Programming Interface** 라고 한다.
즉, DOM API는 **HTML의 요소들을 JS에서 제어하기 위한 명령**들의 집합을 뜻 한다.
> 

### Location

> **`Location`** 인터페이스는 객체가 연결된 장소(URL)를 표현한다. `Location` 인터페이스에 변경을 가하면 연결된 객체에도 반영되는데, `[Document](https://developer.mozilla.org/ko/docs/Web/API/Document)`와 `[Window](https://developer.mozilla.org/ko/docs/Web/API/Window)` 인터페이스가 이런 `Location`을 가지고 있다.
> 

1. Location.href

- 온전한 URL을 값으로 하는 `[DOMString](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String)이다`.
- 바뀔 경우 연결된 문서도 새로운 페이지로 이동한다.
- 연결된 문서와 다른 오리진에서도 설정할 수 있다.
1. Location.host
    - URL의 호스트 부분을 값으로 하는 `[DOMString](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String)`으로, 호스트명, `':'`, 포트 번호를 포함한다.
2. Location.pathname
    - `'/'` 문자 뒤 URL의 경로를 값으로 하는 `[DOMString](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String)이다`
3. Location.search
    - `'?'` 문자 뒤 URL의 쿼리스트링을 값으로 하는 `[DOMString](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String)이다`. 모던 브라우저에서는 `[URLSearchParams.get()](https://developer.mozilla.org/ko/docs/Web/API/URLSearchParams/get)`과 `[URL.searchParams](https://developer.mozilla.org/ko/docs/Web/API/URL/searchParams)`를 사용해서 인자를 쉽게 추출할 수 있다.

### pathname

> `[URL](https://developer.mozilla.org/ko/docs/Web/API/URL)` 인터페이스의 **`pathname`** 속성은 URL의 경로와 그 앞의 `/`로 이루어진 `[USVString](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/String)`을 반환한다. 경로가 없는 경우 빈 문자열을 반환한다.
> 

```jsx
const path = url.pathname;
url.pathname = newPath;

var url = new URL(
  "https://developer.mozilla.org/ko/docs/Web/API/URL/pathname?q=value",
);
var result = url.pathname; // Returns:"/ko/docs/Web/API/URL/pathname"
```