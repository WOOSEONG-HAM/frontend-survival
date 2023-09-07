# 8주차 CSS in JS

# Design System

## 반응형 웹 디자인(Responsive web design)

> 하나의 웹사이트를 PC, 스마트폰, 태블릿 등 다양한 해상도를 가진 디스플레이에 따라 웹페이지 크기가 자동으로 변하도록 만든 웹페이지 접근 기법을 말한다.
웹사이트를 PC용과 모바일용으로 각각 별개로 제작하지 않고, 하나의 웹사이트를 만들어 다양한 디바이스에 대응할 수 있다.
>

### 미디어쿼리

> @media는 지정된 미디어 유형과 장치 유형이 일치하면 미디어 쿼리의 모든 표현식이 참으로 변합니다.
미디어 쿼리가 참일 경우 일반적인 방식(계단식 규칙)에 따라 해당 스타일 시트 또는 스타일 규칙이 적용됩니다. 반응이 빠른 웹 디자인은 html과 css만 사용합니다.
>

## 디자인 시스템(Design System)

> 디자인 시스템은 다양한 페이지와 채널을 걸쳐 공통의 언어와 시각적 일관성을 만들고 반복되는 작업을 줄임으로써, 규모에 맞게 디자인을 관리하기 위한 표준 집합이다.
>

## Atomic Design

> 웹 프론트 개발 프레임워크, 라이브러리인 Angular, Vue, React는 컴포넌트 단위로 개발을 진행한다.
>
>
> 이러한 컴포넌트를 가장 작은 단위로 설정하고 이를 바탕으로 상위 컴포넌트를 만들어 코드 재사용을 최대화하는 방법론이다.
>

# CSS in JS

> CSS-in-JS는 단어 그대로 자바스크립트 코드에서 CSS를 작성하는 방식을 말한다. 2014년 페이스북 개발자인 Christopher Chedeau aka Vjeux가 처음 소개하였다.
>

```jsx
import styled from 'styled-components';

const Text = styled.div`
  color: white,
  background: black
`

<Text>Hello CSS-in-JS</Text>
```

# props와 attrs

## Props

```jsx
//활성화 여부를 표현하거나, 특정 스타일을 잡아주고 싶을 때 유용하다

import { useBoolean } from 'usehooks-ts';

import styled, { css } from 'styled-components';

type ParagraphProps = {
 active?: boolean;
}

const Paragraph = styled.p**<ParagraphProps>**`
 color: ${(**props**) => (props.active ? '#F00' : '#888')};
 ${(**props**) => props.active && **css**`
  font-weight: bold;
 `}
`;

export default function Greeting() {
 const { value: active, toggle } = useBoolean(false);
 
 return (
  <div>
   <Paragraph>
    Inactive
   </Paragraph>
   <Paragraph active>
    Active
   </Paragraph>
   <Paragraph active={active}>
    Hello, world
    <button type="button" onClick={toggle}>
     Toggle
    </button>
   </Paragraph>
  </div>
 );
}
```

## attrs

```jsx
// 기본 속성을 추가할 수 있음. 불필요하게 반복되는 속성을 처리할 때 유용한데, 버튼 등을 만들 때 적극 활용

import styled from 'styled-components';

const Button = styled.button.**attrs**({
 type: 'button',
})`
 border: 1px solid #888;
 background: transparent;
 cursor: pointer;
`;

export default Button;
```

# Global Style & Theme

## Theme

> 테마(Theme)는 우리가 만드는 웹 어플리케이션의 디자인 통일감을 위해서 필요한 기능이다. 만드는 버튼마다 margin, padding, font-size, color가 다 다르면 통일감이 없어보여서 완성도가 떨어지는 느낌을 줄 것이다. 즉 Theme는 styling을 하는데 있어서 필요한 공통 속성을 모아놓은 것이라고 말할 수 있다.
>

## **ThemeProvider**

> **ThemeProvider**는 Styled-Components안에 들어있는 컴포넌트중 하나이다.
>
>
> **ThemeProvider**를 사용하면 하위에 있는 태그들에게 모두 스타일이 미치게되어 전역적으로 스타일링을 해줄 수 있다.
>