# Context

![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSpXQKcVGa_m7RXB5T8M11Az1ZjJUWuH9Uo2JxKjvH5fb5MzlzYFw)

React 어플리케이션에서 데이터는 props를 통해서 위에서 아래로 (부모 -> 자식) 전달됩니다. 하지만 `Context`를 사용하면 `props`을 통해 트리의 모든 부분에 직접 값을 넘겨주지 않고도, 값을 아래쪽으로 공유할수 있습니다.

> 나름 신생아 2018년 3월 30일에 배포가 되었데요.

redux, react-router, styled-components 등이 기존에 이 Context API 를 기반으로 구현이 되어있었습니다.

## Context를 언제 사용할까요?

- 애플리케이션으로 전역적으로 데이터가 사용되야 할 때 사용
- 로그인된 사용자의 정보, 테마, 언어 설정 등... 사용

## 전역 상태 관리

**최악의 구조**
프로젝트에서 전역적으로 사용 하려면 Redux, MobX 같은 라이브러리를 사용하지 않으면 아래와 같은 구조와 비슷하게 구현 해야합니다.

![](https://i.imgur.com/tmOeRAT.png)

> Root 컴포넌트의 state 에는 value 라는 값이 있고, 이 값을 변경시키는 handleSetValue 라는 함수가 있다고 가정해봅시다. value 라는 값은 컴포넌트 F 와 J 에서 보여주고 있고, 이 값을 변화시키는 이벤트는 컴포넌트 G 에서 발생합니다.

1. value 값과 handleSetValue 함수를 props 로 하위 컴포넌트한테 전달
1. value 값은 Root => A =>B => F / Root => H => J
1. handleSetValue 값은 Root => A => B => E => G

   👉 **복잡 유지보수성 낮습니다. hell😵**

**전역 상태관리 적용**
Redux 나 MobX 같은 라이브러리 또는 `Context API`을 통하여 전역 상태관리를 할수 있어요

![](https://i.imgur.com/iyNKCIz.png)

## [실습] 가즈아!!! 😋

![컴포넌트 준비하기](https://i.imgur.com/yXgSkHL.png)

- App 컴포넌트 내부에 LeftPane 과 RightPane 라는 컴포넌트를 만들고
- 한쪽에는 값을 설정시킬 Sends 컴포넌트, 그리고 반대쪽에는 Receives 컴포넌트를 넣어주겠습니다.
- App 에서부터 아래로 props 를 전달하는 것이 아닌, Context 를 통해서 바로 가져와서 사용해보겠습니다.

[실습 참고](https://velopert.com/3606)

---

**실습자료**
[Context](https://codesandbox.io/s/qz138z25q6)
[hoc](https://codesandbox.io/s/v5184zo0y)
[Context많을 경우](https://codesandbox.io/s/6v6pxvkwww)
[hoc 만들는 함수](https://codesandbox.io/s/3v78yz115q)

## API 정리

### React.createContext

`createContext`라는 함수를 호출하면 `Provider` 와 `Consumer` 라는 컴포넌트들이 반환

### Provider

`Provider` 는 `Context` 에서 사용 할 값을 설정할 때 사용

### Consumer

`Consumer` 는 나중에 우리가 설정한 값을 불러와야 할 때 사용

## Context API가 Redux를 대체할 수 있을까요?

[Context API가 Redux를 대체할 수 있을까요?](https://medium.com/@Dev_Bono/context-api%EA%B0%80-redux%EB%A5%BC-%EB%8C%80%EC%B2%B4%ED%95%A0-%EC%88%98-%EC%9E%88%EC%9D%84%EA%B9%8C%EC%9A%94-76a6209b369b)

# 참고한 링크

[React DOCS](https://reactjs-org-ko.netlify.com/docs/context.html)

[velopert Context](https://velopert.com/3606)
