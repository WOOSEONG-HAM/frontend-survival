# 7주차 Routes

## 학습 키워드

- 라우터란?
- React Router
    - Browser Router
    - Route
    - Memory Router

## 라우터란?

> **라우터**란 사용자 요청(URL)에 따라 적절한 컨텐츠를 보여주거나 페이지를 이동시키기 위한 기술이다.
> 

## React Router

> 사용자가 입력한 주소를 감지하는 역할을 하며, 여러 환경에서 동작할 수 있도록 여러 종류의 라우터 컴포넌트를 제공한다.
> 

### Browser Router

> 브라우저 History API를 사용해 현재 위치의 URL을 저장해주는 역할을 해준다.
URL를 읽고, URL을 기반으로 컴포넌트를 렌더링 시켜주거나, 뒤로가기와 같은 사용자 이벤트를 처리하여 UI를 업데이트 한다.
> 

### **Routes /** Route

> **Routes**는 **Route**를 그룹화하기 위해서 사용한다.
어느 위치에서나 **Routes**를 사용할 수 있으며, **Routes**를 사용한 위치(경로)가 베이스가 된다. 
그래서 이는 현재 **path**에 대한 하위 **path Route**의 집합이라 할 수 있다.
URL이 변경되면 Routes는 하위 Route를 탐색하여 가장 일치하는 path를 찾아 컴포넌트를 렌더링한다.
> 

```jsx
<Routes>
	<Route path='/' element={<HomePage />} />
	<Route path='/about' element={<AboutPage />} />
</Routes>
```

### **Memory Router**

메모리 라우터는 메모리 상에서 라우팅을 처리하는 역할을 한다.

테스트 환경에서는 브라우저를 사용하지 않기 때문에, 브라우저 라우터 대신에 메모리 라우터를 사용한다.

브라우저는 메모리에다가 path를 써주지만 메모리 상에서는 그런게 없기 때문에 path를 설정해줘야 한다.

`initialEntries`는 테스트할 path를 설정해줄 수 있으며, 값은 배열 형태로 들어가야 한다.

```jsx
describe('App', () => {

	context('when the current path is "/"', () => {

		it('renders the home page', () => {

			render((

				<MemoryRouter initialEntries={['/']}>

					<App />

				</MemoryRouter>

			));

			screen.getByText(/Welcome/);

		});

	});

});
```