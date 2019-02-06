### defaultProps

실수로 props를 빠트릴경우 props의 기본값을 설정해줄 수 있습니다. 바로 default Props이다.

```js
import React, { Component } from "react";

class MyName extends Component {
  static defaultProps = {
    name: "기본이름"
  };
  render() {
    return (
      <div>
        안녕하세요! 제 이름은 <b>{this.props.name}</b> 입니다.
      </div>
    );
  }
}

export default MyName;
```

---

### State

동적인 데이터를 다룰 때 state를 사용합니다.

```js
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = {
      number: 0
    }
  }
```

constructor에서 `super(props)`를 호출 한 이유는, 우리가 컴포넌트를 만들게 되면서, Component를 상속했으며, 우리가 이렇게 constructor를 작성하게 되면 기존의 클래스 생성자를 덮어쓰게 됩니다. 리액트 컴포넌트가 가지고있던 생성자를 super를 통하여 미리 실향하고 state 설정을 해주는것입니다.

`State`는 props와 비슷하지만 바깥으로 공개되지 않으며, 컴포넌트에 의해 완전히 제어됩니다.
클래스로 정의한 컴포넌트에는 몇가지 추가 기능이 있습니다. 지역적인 state가 바로 그러한 기능으로, 클래스에서만 사용 가능합니다.

클래스 컴포넌트는 항상 `props`를 가지고 상위 생성자를 호출해야만 합니다.

---

### setState

`this.setState((이전 상태) => ({ 이름: 바꿀 값 }));`

각 메소드에 들어있는 `this.setState`. state에 있는 값을 바꾸기 위해서는 this.setState를 무조건 거쳐야합니다. 리액트에서는, 이 함수가 호출되면 컴포넌트가 리렌더링 되도록 설계되어있습니다.

setState는, 객체로 전달되는 값만 업데이트를 해줍니다.

자바스크립트의 전개연산자 입니다. 기존의 객체안에 있는 내용을 해당 위치에다가 풀어준다는 의미죠. 그 다음에, 우리가 설정하고 싶은 값을 또 넣어주면 해당 값을 덮어쓰게 됩니다.

이러한 작업이 꽤나 귀찮으므로, 나중에는 `immutable.js` 혹은 `immer.js` 를 사용하여 이 작업을 좀 더 간단하게 해줍니다.

#### setState에 객체 대신 함수를 전달

**비구조화 할당**

```js
const { number } = this.state;
this.setState({
  number: number + 1
});
```

---

### State 바르게 사용하기

1. **state를 직접 수정하지 마세요.**
   ```js
   // Wrong
   this.state.comment = "Hello";
   ```
   `setState()` 를 사용하세요.
   ```js
   // Correct
   this.setState({ comment: "Hello" });
   ```
   this.state를 할당할 수 있는 유일한 장소는 생성자 함수 내부입니다.
1. **state 업데이트는 비동기일 수 있습니다.**
   React는 성능을 위해 여러 `setState()` 호툴을 한번의 작업으로 묶어서 처리하는 경우가 있습니다.
   `this.props` 및 `this.state`가 비동기로 업데이트될 수 있기 때문에, 다음 state를 계산할 때 이 값을 신뢰해서는 안됩니다.
   `setState()`를 사용할 수 있습니다. 이 함수는 이전 state를 첫번째 인수로 받고, 두번 째 인수로 업데이트가 적용 될때 props를 받습니다.
   ```js
   // Correct
   this.setState(function(prevState, props) {
     return {
       counter: prevState.counter + props.increment
     };
   });
   ```
1. **state 업데이트는 병합됩니다.**
   `setState()` 를 호출할 때, React는 넘겨받은 객체를 현재 state에 병합니다.
   state는 여러 독립적인 변수를 가질 수 있습니다.

   ```js
   constructor(props) {
   super(props);
   this.state = {
     posts: [],
     comments: []
   };
   }
   ```

   `setState()`를 호출하여 아이템을 각각 업데이트할 수 있습니다.

   ```js
     componentDidMount() {
    fetchPosts().then(response => {
      this.setState({
        posts: response.posts
      });
    });

    fetchComments().then(response => {
      this.setState({
        comments: response.comments
      });
    });
   }
   ```

---

### 데이터는 아래로 흐릅니다.

부모 컴포넌트나 자식 컴포넌트는 특정 컴포넌트의 state 유무를 알 수 없으며, 해당 컴포넌트가 함수나 클래스로 선언되었는지 알 수 없습니다.

state가 '지역적이다.' 혹은 '캡슐화되었다'고 하는 이유입니다. State를 지정해 준 컴포넌트 외의 다른 컴포넌트에서는 state에 접근할 수 없습니다.

컴포넌트는 자신의 state를 props로서 작식 컴포넌트에 내려줄 수 있습니다.

이런한 데이터 흐름을 보통 `하향식` 혹은 `단방향` 데이터 흐름이라고 합니다.
컴포넌트 트리를 props의 폭포라고 상상하면 됩니다. 임의의 지점에서 추가되는 물과 비슷하고 또한 아래로 흐릅니다.
