# 9주차 온라인 쇼핑몰

## 개발하기 전 준비

### 용어

- Product: 상품
  - Summary: 상품에 대한 요약 정보
  - Detail: 상품에 대한 상세 정보
  - Image: 상품 이미지
  - Option: 상품에 대한 상세 옵션 종류 (색상, 크기 등)
    - OptionItem: 옵션에 대한 상세 옵션 값 (옵션이 색상이라면 이건 Blue, Red 같은 걸 의미함)
- Category: 상품에 대한 분류
- Cart: 장바구니
  - LineItem: 장바구니에 담긴 것 (상품, 옵션, 수량 등을 동시에 다룸)
    - 여기서도 Option과 OptionItem을 사용한다.
    - 용어는 동일하지만 Product와 다른 구성을 갖기 때문에, 여기서는 Product와 Order라는 접두어를 활용한다.
    - 시스템을 분리할 수 있다면, 근본적으로 나누는 걸 추천(상품 정보 확인 / 장바구니 / 주문).
- Order: 주문
  - 여기서도 동일한 LineItem 활용.
- User: 사용자

### 기능

1. 상품 목록 확인
2. 상품 상세 정보 확인
3. 장바구니에 상품 담기
4. 주문하기 → 배송지 입력, 결제
5. 주문 목록 확인
6. 주문 상세 확인
7. 로그인
8. 회원 가입

### 화면

1. 홈 페이지 - `/`
2. 상품 목록 페이지 - `/products`
3. 상품 상세 페이지 - `/products/{id}`
4. 장바구니 페이지 - `/cart`
5. 주문 페이지 - `/order`
6. 주문 완료 페이지 - `/order/complete`
7. 주문 목록 페이지 - `/orders`
8. 주문 상세 페이지 - `/orders/{id}`
9. 로그인 페이지 - `/login`
10. 회원 가입 페이지 - `/signup`
11. 회원 가입 완료 페이지 - `/signup/complete`

### E2E Test

> E2E(End to End) 테스트는 개발물을 사용자 관점에서 테스트 하는 방법이다. 페이지에서 원하는 텍스트가 제대로 출력이 되었는지, 버튼을 클릭 했을 때 올바른 동작을 수행하는 지 등을 테스트한다.
>
- **Endpoint(종단)** 간 테스트로 **사용자의 입장에서 사용자가 사용하는 상황**을 가정하고 테스트 하는 것
- 일반적으로 웹이나 어플 등에서 GUI를 통해 시나리오, 기능 테스트 등을 수행한다.
- 사용자에게 직접적으로 노출되는 부분을 점검한다.
- 유닛 테스트로 불가능한 **사용자 관점의 테스트**까지 가능하다.
- Endpoint 테스트를 통과하면 기능이 잘 작동한다는 것이므로 모든 테스트를 할 수 없다면 **E2E Test만이라도 하자.**
- **백엔드 관점**에서 개발한 **REST API를 테스트** 하기 위해 실제로 서버에 요청을 보낸 뒤 클라이언트에서 원하는 데이터가 전송되는 지 확인해야 한다.

### CodeceptJS

> CodeceptJs는 BDD 방식으로 누구나 보기 쉬운 E2E 테스트를 각자의 시나리오에 따라 좋은 가독성을 제공해준다.
>

### MSW

> MSW(Mock Service Worker의 약자, [https://mswjs.io](https://mswjs.io/))는 API Mocking 라이브러리로, 서버향의 네트워크 요청을 가로채서 모의 응답(Mocked response)을 보내주는 역할을 한다. 따라서, Mock Service Worker(MSW) 라이브러리를 통하면, Mock 서버를 구축하지 않아도 API를 네트워크 수준에서 Mocking 할 수 있다.
>

```jsx
// REST API 스펙에 맞춰서 MSW 핸들러를 준비

import { rest } from 'msw';

import { ProductSummary } from '../types';

import fixtures from '../../fixtures';

const BASE_URL = 'https://shop-demo-api-01.fly.dev';

const productSummaries: ProductSummary[] = fixtures.products
  .map((product) => ({
    id: product.id,
    category: product.category,
    thumbnail: { url: product.images[0].url },
    name: product.name,
    price: product.price,
  }));

const handlers = [
  rest.get(`${BASE_URL}/categories`, (req, res, ctx) => (
    res(ctx.json({ categories: fixtures.categories }))
  )),
  rest.get(`${BASE_URL}/products`, (req, res, ctx) => (
    res(ctx.json({ products: productSummaries }))
  )),
  rest.get(`${BASE_URL}/products/:id`, (req, res, ctx) => {
    const product = fixtures.products.find((i) => i.id === req.params.id);
    if (!product) {
      return res(ctx.status(404));
    }
    return res(ctx.json(product));
  }),
  rest.get(`${BASE_URL}/cart`, (req, res, ctx) => (
    res(ctx.json(fixtures.cart))
  )),
  rest.post(`${BASE_URL}/cart/line-items`, (req, res, ctx) => (
    res(ctx.status(201))
  )),
];

export default handlers;
```
