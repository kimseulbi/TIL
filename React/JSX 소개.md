# JSX 소개

```js
const element = <h1>Hello, world!</h1>;
```

이 문법은 JSX라고 부르며, 자바스크립트의 확장 문법입니다. JSX를 리액트와 함께 사용하면, UI가 실제로 어떻게 보일지 서술할 수 있습니다. JSX는 오로지 자바스트립트를 기반으로 동작한다.

React 렌더링 로직 = 이벤트의 처리 과정, 시간에 따른 상태 변화, 표시할 데이터가 어디로부터 오는지가 **렌더링 로직**과 결합되어 있다.

많은 사람들은 자바스크립트 코드 안에서 UI 작업을 할때 시각적으로 더 편하다고 합니다.

### jsx에 표현식 포홤하기

```js
function formatName(user) {
    return user.firstName + '' + user.lastName;
}
const user = {
    firstName: 'Harper',
    lastName: 'Perez'
};

const element = (
    <h1>
        Hello, {formatName(user)}!
    </h1>
);

ReactDOM.render(
  element,
  document.getElementById('root')

// Hello, Harper Perez!
```

컴파일이 끝나면, JSX 표현식이 일반적인 자바스크립트 함수 호출이 되고, 결과적으로 자바스크립트 객체로 평가된다.

`if`문이나 `for`문 내에서 JSX를 사용할 수 있으며, 변수에 할당하거나 매개변수로 전달하거나 함수에서 반환할 수 있을을 의미한다.

```js
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

### JSX 어트리뷰트 정의

따옴표를 사용해서 문자열 리터럴 정의

```js
const element = <div tabIndex="0" />;
```

중괄호를 사용하면 , 자바스크립트 표현식을 포함

```js
const element = <img src={user.avatarUrl} />;
```

> JSX`class`는 `className`이 되면 `tabindex`는 `tabIndex`가 됩니다.

### JSX자식 정의

태그가 비어있다면, XML 처럼 /> 를 이용해 닫아주어야 합니다.
그냥 html 태그에서 자식 갖는거랑 같음.

```js
const element = <img src={user.avatarUrl} />;
// JSX 태그는 자식을 가질 수 있습니다.
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

### JSX 인젝션 공격 예방???

사용자가 입력한 내용을 JSX 내에 포함시켜도 안전합니다.

기본적으로, React DOM은 렌더링 되기 전에 JSX 내에 포함된 모든 값을 이스케이프 합니다. 따라서 어플리케이션에 명시적으로 작성되지 않은 내용은 절대 삽입할 수 없습니다. 모든 것은 렌더링 되기 전에 문자열로 변환됩니다. 이렇게 하면 XSS (cross-site-scripting) 공격을 막을 수 있습니다.

```js
const title = response.potentiallyMaliciousInput;
// This is safe:
const element = <h1>{title}</h1>;
```

> XSS (cross-site-scripting) \
> 쉽게 말하면 해커가 자바스크립트 코드를 웹페이지에 심어 사용자의 정보를 탈취하는 종류의 공격이다. 일반적으로 웹 어플리케이션들은 사용자로부터 데이터를 입력받게 되는데 이 데이터에 해커가 자바스크립트 코드를 심어 놓을 수 있는 것이다. 쉽게 생각해 게시판에 글을 쓴다고 생각해보자. 글 내용에 해커가 자바스크립트 코드를 심어 놓고 사용자들이 이 글을 보면서 동시에 자바스크립트 코드가 실행되어 해커가 원하는 것을 얻을 수 있게 된다. 물론 이런 공격은 많이 알려져 있기 때문에 대부분에 이와 같은 입력은 사전에 필터링을 통해 차단한다

### JSX 객체 표현

Babel은 JSX를 `React.createElement()` 호출로 컴파일합니다.

```js
const element = <h1 className="greeting">Hello, world!</h1>;
```

`React.createElement()`는 버그 없는 코드를 작성하는 데 도움을 주는 몇 가지 체크를 하긴 하지만, 기본적으로는 아래와 같은 객체를 생성합니다.

```js
// Note: this structure is simplified
const element = {
  type: "h1",
  props: {
    className: "greeting",
    children: "Hello, world"
  }
};
```

이 객체를 “React 요소”라고 부릅니다. React는 이 객체를 읽어들이고 이를 사용하여 DOM을 만들어낸 뒤 최신 상태로 유지합니다.

> ES6 및 JSX 코드가 모두 올바르게 표시되도록 선택한 편집기에 “Babel” 언어 설정 을 사용하는 것이 좋습니다.
