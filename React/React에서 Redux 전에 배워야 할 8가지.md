# React에서 Redux전에 배워야 할 8가지

### React에 Redux를 사용하기 전에 알아야할 사실들, 번역

이 글은 Robin Wieruch의 [8 things to learn in React before using Redux](https://www.robinwieruch.de/learn-react-before-using-redux/)번역입니다.

## React에서 Redux 전에 배워야 할 8가지

상태 관리는 어렵습니다. React같은 뷰 라이브러리는 지역 컴포넌트 상태를 관리하는 일이 가능합니다. 하지만 이 상태느 특정 시점에서 확장해야 하는 일이 생깁니다. 리엑트는 단순히 뷰 계층 라이브러리 입니다. 언젠가는 Redux와 같이 더 수준 높은 상태 관리 솔루션으로 넘어가는 결정을 하게 될 겁니다. 하지만 이 글에서는 Redux 열차에 올라타기 전에 React에서 알아야 하는 부분에 대해서 지적하고 싶습니다.

사람들은 간혹 React와 Redux를 함께 배웁니다. 하지만 거기에 문제점이 있습니다.

- 지역 상태(this.state)만 사용하는 경우에 왜 상태 관리에 확장 문제가 발생하는지 겪어보지 못합니다.
  - 그래서 왜 Redux 같은 상태 관리 라이브러리가 필요한지 이해하지 못합니다.
  - 그래서 너무 많은 보일러플레이트에 대해 불평합니다.
- React에서 지역 상태를 관리하는 방법을 배우지 못합니다.
  - 그래서 모든 상태를 Redux에서 제공하는 상태 컨테이너에 담아두고 관리하려고 합니다.
  - 그래서 지역 상태 관리를 전혀 사용하지 않게 됩니다.

이런 문제점으로 인해서 React를 먼저 배우고 나중에 필요하다고 느낄 때 Redux를 배우도록 조언합니다. 확장 문제는 대형 애플리케이션에서만 나타납니다. 가끔 Redux를 사용하고 있으면서도 상태 관리 라이브러리가 필요하지 않은 경우가 있습니다. 책 The Road to learn React에서는 Redux와 같은 외부 의존성 없이 있는 그대로의 React로 애플리케이션을 만드는 방법을 설명합니다.

하지만 당신은 지금 Redux 열차에 올라타기로 결정했습니다. 그래서 이 글에서는 Redux를 쓰기 전에 React에서 알아야 할 내용을 살펴봅시다.

1. React에서의 지역 상태는 자연스럽다.
1. React 함수형 지역 상태
1. React의 상태와 프로퍼티
1. React 상태 옯기기
1. React의 고차 컴퍼넌트
1. React의 Context API
1. React의 상태 컴포넌트
1. 컨테이너와 프레젠터 패턴
1. MobX 아니면 Redux?

## React에서의 지역 상태는 자연스럽다.

이미 언급했지만 가장 중요한 조언은 React를 먼저 학습하라는 점입니다. 컴포넌트에 지역 상태 즉, `this.setState()`와 `this.state`를 사용해서 생명을 붙어 넣는 일을 피할 수없습니다. 이 방식에 익숙해져야 합니다.

```js
class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = { counter: 0 };
  }
  render() {
    return (
      <div>
        Counter:{this.state.counter}
        <button
          type="button"
          onClick={() => this.setState({ counter: this.state.counter + 1 })}
        >
          Click!
        </button>
      </div>
    );
  }
}
```

React 컴포넌트는 초기 상태를 생성자(constructor)에서 정의하고 있습니다. 그런 후에 `this.setState()`메소드를 사용해서 갱신할 수 있습니다. 상태 객체의 갱신은 얕은 병합(shalloq merge)으로 수행됩니다. 그러므로 지역 상태 객체를 부분적으로 갱신하고도 상태 객체의 다른 프로퍼티는 송대지 않고 대로 유지할 수 있습니다. 상태가 갱신된 후에는 컴포넌트가 다시 렌더링을 수행합니다. 앞에서 예로 든 코드에서는 `this.state.counter`의 갱신된 값을 보여줄 것입니다. 이 에제에서는 React의 단 방향 데이터 흐름을 사용해 하나의 닫힌 루프를 작성했습니다.

## React 함수형 지역 상태

`this.setState()`메소드는 지역 상태를 비동기적으로 갱신합니다. 그러므로 언제 상태가 갱신되는지에 대해 의존해서는 안됩니다. 상태 갱신은 결과적으로 나타납니다. 대부분의 경우에는 이런 방식이 별 문제 없습니다.

하지만 컴포넌트의 다음 상태를 위해 연산을 하는데 현재 지역 상태에 의존한다고 가정해봅시다. 앞서 작성했던 예제에서는 다름처럼 작성했습니다.

```js
this.setState({ counter: this.state.counter + 1 });
```

지역 상태(`this.state.counter`)는 연산에서 바로 그 시점의 상태로 사용했습니다. 그러므로 `this.setState()`를 사용해서 상태를 갱신하긴 했지만 지역 상태는 비동기 실행이 수행되기 전에 신선하지 않은 상태값을 사용해 연산하게 됩니다. 이런 점은 처음 보고 나서는 바로 파악하기 어렵습니다. 천 마디 말 보다 다음 코드를 보는게 더 빠를 것 같습니다.

```js
this.setState({ counter: this.state.counter + 1 }); // this.state: { counter: 0 }
this.setState({ counter: this.state.counter + 1 }); // this.state: { counter: 0 }
this.setState({ counter: this.state.counter + 1 }); // this.state: { counter: 0 }

// 예상한 상태: { counter: 3 }
// 실제 갱신된 상태: { counter: 1 }
```

이 코드에서 확인할 수 있는 것처럼 지역 상태를 갱신할 때 현재 상태에 의존해서는 안됩니다. 이런 접근방식은 버그를 만듭니다. 그래서 이런 상황에서는 다음과 같은 방식으로 지역 상태를 갱신합니다.

`this.setState()`에는 객체 대신 함수도 사용할 수 있습니다. 함수는 비동기적으로 `this.setState()`가 실행될 때, 함수 시그니처에 지역 상태를 전달합니다. 그래서 이 함수는 콜백 함수로 정확한 시점에 올바른 상태를 갖고 실행되기 떄문에 문제 없이 사용할 수 있게 됩니다.

```js
this.setState(previousState => ({ counter: previousState.counter + 1 }));
```

이 방법으로 `this.setState()`를 여전히 이용하면서도 객체 대신 함수를 사용해서 이전 상태를 활용 할 수 있습니다.

추가적으로 프로퍼티(props)에 의존적인 갱신이 필요한 경우에도 이 접근 방식을 따라야 합니다. 비동기적 실행이 수행되기 이전에 부모 컴포넌트에서 받은 프로퍼티가 변역되어서 값이 이전 정보가 되는 경우가 있기 때문입니다. 그래서 `this.setState()`의 두번째 인자로 프로퍼티가 전달됩니다.

```js
this.setState((prevState, props) => ...);
```

이제 올바른 상태와 프로터피를 사용해서 상태를 갱신할 수 있게 됩니다.

```js
this.setState((prevState, props) => ({
  counter: prevState.counter + props.addition
}));
```

## 객체 개신에 함수를 사용하면서 얻을 수 있는 또 다른 장점은 바로 상태를 갱신하는 방법을 격리된 상태에서 테스트 해볼 수 있다는 점입니다. 단순히 `this.setState(fn)`을 사용하는 함수를 추출한 다음에 독립적으로 둔 다음에 테스트가 가능하도록 작성할 수 있습니다. 이 함수는 입력으로 간단히 출력을 확인할 수 있는 순수 함수여야 합니다.

출처:
https://edykim.com/ko/post/learn-react-before-using-redux/?fbclid=IwAR29TU8sYX5ttzG2zt2wefdNFLCinLJwj4s076Gm-UkXT8xbHaS_rTnczGs
