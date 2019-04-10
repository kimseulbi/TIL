# ImmutableJS Immer

가변성과 불변성 차이 - 원시타입과 참조타입

원시타입은 객체(배열)

```js
import produce from "immer";

const todos = [
  { text: "아구찜 먹기", done: false },
  { text: "브래드피트 사진 보기", done: false }
];

// draft: producer 함수는 현재 상태의 대신하는 draft를 인자로 받는다.
// 반환값이 produce 조작된 draft 입니다.

const nextTodos = produce(todos, draft => {
  draft.push({ text: "Immer 배우기", done: true });
  draft[1].done = true;
});

// old state is unmodified
console.log(todos.length); // 2
console.log(todos[1].done); // false

// new state reflects the draft
console.log(nextTodos.length); // 3
console.log(nextTodos[1].done); // true

// structural sharing
// 메모리 보존
console.log(todos === nextTodos); // false
console.log(todos[0] === nextTodos[0]); // true
console.log(todos[1] === nextTodos[1]); // false
```

```js
//states는 객체
produce(state, draft => {
  switch (action.type) {
    case RECEIVE_PRODUCTS:
      action.products.forEach(product => {
        // 이름으로 표기 하기위해 []
        draft[product.id] = product;
      });
      break;
  }
});
```

default 케이스에 대한 처리도 필요가 없어졌다. 드래프트에 변경을 가하지 않으면 기본 상태가 그대로 반환
