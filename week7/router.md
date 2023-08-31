# 7주차 Router

## 학습 키워드

- ReactRouter - RouterProvider

## RouterProvider

> `React Router v6.4`에 추가된 방식이다.
>

```jsx
// 기존 방식
import { BrowserRouter } from 'react-router-dom'

const root = ReactDOM.createRoot(document.getElementById('root'))
root.render(
  <BrowserRouter> // 최상단 root에서 BrowserRouter로 감싸기
      <App /> 
  </BrowserRouter>
)
```

```jsx
// 기존 방식
import { Route, Routes } from 'react-router-dom'

const App = () => {
  return (
    <Routes>
      <Route path='/' element={<Layout />} > // outlet을 이용한 중첩라우팅
        <Route index element={<Main />} /> 
        <Route path='/pageA' element={<PageA />} />
        <Route path='/pageB' element={<PageB />} />
        <Route path='/pageC' element={<PageC />} />
      </Route>
      </Routes>
  )
}
```

### **router.jsx**

> 기존 방식과는 다르게 새로운 컴포넌트를 만들어서 route 링크 들만 따로 분리를 시켜서 관리할 수 있다.
>
>
> 기존 구성에서 중첩 되어있는 경로는 children을 이용해서 중첩을 사용할 수 있다.
>

```jsx
import Layout from '../Layout'
import Main from '../pages/Main';
import AboutPage from '../pages/AboutPage';

export const RouterInfo = [
  {
    path: "/",
    element: <Layout />,
    children: [
      {
        index: true,
        element: <Main />,
        label: 'main'
      },
      {
        path: "/AboutPage",
        element: <AboutPage />,
        label: 'About'
      },
    ]
  },
]
```

### **createBrowserRouter & RouterProvider**

> 기존 방식처럼 BrowserRouter로 감싸지 않고 RouterProvider를 이용해서 구성요소들을 전달하고 활성화 한다.
>

```jsx
import { createBrowserRouter, RouterProvider, } from 'react-router-dom';
import { RouterInfo } from './util/router';

const RouterObject = createBrowserRouter(RouterInfo) 
//CreateBrowserRouter로 경로 지정

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <RouterProvider router={RouterObject} />
  </React.StrictMode>
);
```

[Feature Overview v6.15.0](https://reactrouter.com/en/main/start/overview)
