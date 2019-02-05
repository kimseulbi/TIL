# 컴포넌트와 Props

컴포넌트를 통해 UI를 독립적으고 재사용 가능한 부분을 분리하고, 각 부분을 독립적으로 생각

개념상 컴포넌트는 자바스크립트 함수와 비슷 `props`이라 불리는 임의의 입력을 받아들이고, 화면에 무엇이 표시되어야 하는지를 서술하는 React 요소를 반환합니다.

### 함수형 및 클래스 컴포넌트

컴포넌트를 정의하는 가장 간단한 방법은 **자바스크립트 함수로 작성**

> 🏷 **자바스크립트**는 **객체기반의 스크립트**프로그래밍언어이다. 이언느 웹 즈라우저 내에서 주로 사용하며, 다른 응용 프로그램 내장 객체에도 접근할 수 있는 기능을 가지고 있다.

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

이 함수는 유효한 React 컴포넌트로 `props` 객체 인수를 받고 React 요소를 반환합니다. 이러한 컴포넌트는 자바스크립트 함수이기 때문에 `함수형 컴포넌트`라고 부릅니다.

컴포넌트를 정의하기 위해 `ES2015 class`를 사용할 수 있습니다.

```js
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

두 컴포넌트는 React 관점에서 봤을때 동일한 기능을 갖습니다.

### 컴포넌트 렌더링

```js
const element = <Welcome name="Sara" />;
```

React가 사용자 정의 컴포넌트를 나타내는 요소를 처리할 때는, JSX 어트리뷰트를 하나의 객체를 통해 컴포넌트로 전달합니다. 이 객체를 `props`라고 부릅니다.

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(element, document.getElementById("root"));
```

> `<div />`는 DOM 태그를 나타내지만 `<Welcome />`은 컴포넌트를 나타내며 스코프에 `Welcome`이 있어야합니다.

### 컴포넌트 조립

컴포넌트의 출력에서 다른 컴포넌트를 가져와 사용할 수 있습니다. 모든 세부 레벨에서 동일한 컴포넌트 추상화를 사용.

예를 들어 `Welcome`을 여러번 렌더링하는 `APP` 컴포넌트를 만들 수 있습니다.

```js
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(<App />, document.getElementById("root"));
```

일반적으로, React 앱은 단일 `APP` 컴포넌트를 최상위에 둡니다.

### 컴포넌트 추출

```js
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img
          className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">{props.author.name}</div>
      </div>
      <div className="Comment-text">{props.text}</div>
      <div className="Comment-date">{formatDate(props.date)}</div>
    </div>
  );
}
```

몇가지 컴포넌트를 추출합니다.
`Avatar`를 추출할 수 있습니다.

```js
function Avatar(props) {
  return (
    <img className="Avatar" src={props.user.avatarUrl} alt={props.user.name} />
  );
}
```

속성 이름을 지을 때는, 컴포넌트가 사용되는 상황이 아닌 컴포넌트 그 자체만 생각하는 것이 좋습니다.

```js
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <Avatar user={props.author} />
        <div className="UserInfo-name">{props.author.name}</div>
      </div>
      <div className="Comment-text">{props.text}</div>
      <div className="Comment-date">{formatDate(props.date)}</div>
    </div>
  );
}
```

컴포넌트를 추출은 재사용 가능한 컴포넌트 팔레트를 사용하면 큰 앱에서 그 진가를 발휘합니다. 적당한 기준을 잡아보자면, UI의 일부분이 여러 번 사용되거나 , 자체적으로 충분히 복잡하다면, 그것들은 재사용 가능한 컴포넌트가 될 좋은 후보입니다.

### props는 읽기전용

컴포넌트를 `함수나 클래스` 중 어떤 걸로 선언 했던, 자기 자신의 props를 수정 할 수 없습니다.

```js
function sum(a, b) {
  return a + b;
}
```

위와 같은 함수는 입력을 변경하려 하지 않고, 동일한 입력에 대해 항상 동일한 결과를 반환하기 때문에 `순수함수`라고 불립니다.

**모든 React 컴포넌트는 props에 대해서는 순수 함수처럼 동작해야합니다.**
