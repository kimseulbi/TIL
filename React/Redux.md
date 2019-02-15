# Redux

> Flux(상태관리) 영향으로 받을걸로 Redux를 만들었습니다.

**리덕스**

컴포넌트 상태를 공유하게 될 때 여러 컴포넌트를 거치지 않고도 손쉽게 상태 값을 전달

Redux는 React만 사용할수 있는것은 아닙니다.

## 기초 언어

### 액션

그냥 객체입니다. 스토어가 변화를 일으켜야하는 설명서.
데이터의 객체이다.

액션은 애플리케이션에서 스토어로 보내는 데이터 묶음입니다(객체). 우리는 상태가 변경되어야할 때 액션이란 것을 발생시켜야합니다. 스토어에서(정확히 말하자면 리듀서에서) 이 액션을 받아서, 어떠한 변화를 일으켜야하는지에 대한 정보를 참고하여 실제 변화를 일으키게되기 때문입니다

payload: 옵션

### 액션생성자

액션생성자는 단지 액션을 만드는 함수일 뿐, 액션이 아님을 유의하세요.

## dispatch(디스패치)

스토어의 내장함수입니다.

이 액션을 어떻게 보내주느냐, 바로 그 역할을 하는 아이입니다. 디스패치가 보내지면 실제로 액션을 참조하여 로직을 실행하는 동작이 발생되니 액션을 발생시키는 것으로 생각하는 것이죠.

액션을 디스패치한다 -> 상태를 바꿔주는 일이 생긴다. 하지만 디스패치가 상태가 바꿔주는 행동을 해주는것은 아니다. ( 전달 하는 기능 )

redux를 대부분 react와 함께 쓸 것이기 때문에 보통은 connect()를 통해 접근하면 되고

**바인드된 액션 생성자**
액션을 만듬과 동시에 자동으로 액션을 보내주는것

### 리듀서

리듀서는 상태 변화를 실제로 일으키는 함수입니다. dispatch로 action를 전달받아 이 action를 참조해서 변화를 일으킨다

액션을 참고해서 리두서를 만듭니다.

```js
function reducer(prevState, action) {
  // 상태 업데이트 로직
  return newState;
}
```

`reduce` 메소드와 연관이 있어서 리듀서라고 만든거 같음

- 인수들을 변경(mutate)하기;
- API 호출이나 라우팅 전환같은 사이드이펙트를 일으키기;
- Date.now()나 Math.random() 같이 순수하지 않은 함수를 호출하기.

**`순순 함수이여야합니다.`**

리덕스는 `switch`문으로 작성합니다.

1. state 초기 설정을 해줘야한다.
1. 인수를 변경해선 안된다.

> `Object.assign` : 첫번째 객체를 복사하는것

```js
const initialState = {
  drink: '',
  size: '',
  whipping: ''
}

function order(state = initialState, action){
  switch(action.type){
    case "ICE_CHOCO_GRANDE":
      return Object.assign({}, state, {
          drink: '아이스초코',
          size: 'grande',
          whipping: action.whipping
      })
    case "MINT_CHOCO_SAMLL":
      return {
          // 상태가 지워지면 안되기 때문에 복사는 한것
        ...state,
        drink: '아이스초코',
        size: 'grande',
        whipping: action.whipping
      }
    default:
      return state
}

```

짚고 넘어갈 점은:

1. 우리는 state를 변경하지 않았습니다. Object.assign()을 통해 복사본을 만들었죠. Object.assign(state, { drink: '아이스초코', size: 'grande', whipping: action.whipping })이라고 써도 여전히 틀립니다: 첫번째 인수를 변경하게 되니까요. 여러분은 반드시 첫번째 인수로 빈 객체를 전달해야 합니다. ES7로 제안된 object spread syntax을 써서 { ...state, ...newState }로 작성할수도 있습니다.

2) default 케이스에 대해 이전의 state를 반환했습니다. 알 수 없는 액션에 대해서는 이전의 state를 반환하는것이 중요합니다.

## 스토어

`getState()`

현재 스토어에 있는 상태에 접근하는 함수입니다.

`subscribe`

상태가 바뀔 떄마다 실행할 함수를 등록하는 절차
반환값으로 구독을 끊어주는 함수를 반환하기 때문에, 구독을 중지하려면 반환값을 호출하면 됩니다.

## 리덕스의 3가지 규칙

1. 하나의 애플리케이션 안에는 하나의 스토어가 있습니다.
1. 상태는 읽기전용 입니다.
   Object.assign 을 사용하거나 spread 연산자 (...) 를 사용하여 업데이트 하곤 하죠.
1. 변화를 일으키는 함수, 리듀서는 순수한 함수여야 합니다.

`mapStateToProps`

반환값은 객체입니다.

`mapDispatchToProps`

연동될 컴포넌트가 상태를 바꾸기위해 사용할 함수를 컴포넌트에게 props로 전달해줍니다. 여기서 '상태를 바꾸기 위해 사용할 함수'란, 자동으로 dispatch되는 액션 생성자를 뜻합니다. 아~까~ 봤던 바인딩된 액션 생성자인 셈이죠.

mapDispatchToProps가 자동으로 Dispatch가 됩니다.

```js
// 액션생성자를 디스패칭하는 함수를 props로 전달
const mapDispatchToProps = (dispatch, ownProps?) => {
  return {
    increment: () => dispatch(increment()),
    decrement: () => dispatch(decrement())
  };
};
```

`bindActionCreators()`

액션 생산자들로 이루어진 객체를 받아서, 같은 키를 가지지만 각각의 생산자들을 dispatch로 감싸서 바로 호출 가능하게 만든 객체로 바꿉니다.
