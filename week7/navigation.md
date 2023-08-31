# 7주차 Navigation

## 학습 키워드

- Web APIs - History
- React Router - NavLink, Link, Navigate, useNavigate

## Web APIs - History

> **History API**는 브라우저가 관리하는 세션 히스토리(session history), 즉 페이지 방문 이력을 제어하기 위한 웹 표준 API 이다. 여기서 세션은 브라우저마다 살짝 다를 수 있지만 보통 사용자가 새 창이나 탭을 열 때 생성되고 해당 창이나 탭을 닫을 때 소멸한다.
> 
> 
> 브라우저에서 새 탭을 열면 “뒤로 가기”와 “앞으로 가기” 버튼이 비활성화 되어 있을 것 이다. 이 것은 현재 세션 히스토리가 비어있다는 뜻이고 방문 이력을 하나도 없기 때문에 뒤로 가거나 앞으로 갈 페이지가 없다는 뜻이다.
> 
> 자바스크립트에서 History API는 기본적으로 `history` 전역 객체를 통해서 사용해 볼 수 있으며 `window`나 `document` 전역 객체를 통해서도 접근할 수 있다. 예를 들어서, 현재 세션에서 얼마나 많은 페이지를 방문했는지 알고 싶다면 다음과 같이 History API에서 제공하는 `length` 프로퍼티에 접근하면 된다.
> 

## React Router - NavLink, Link, Navigate, useNavigate