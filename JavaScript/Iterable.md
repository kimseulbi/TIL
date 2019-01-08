# Iteration(이터레이션)

Iteration 프로토콜에는 두가지 프로토콜이 있다. 한기지는 `iterable 프로토콜`이고 또 다른 한가지는 `iterator 프로토콜`이다.
ES2015에서 추가된 이 두 가지는 새로운 빌트인 혹은 구문이 아닌 프로토콜 즉, 규약이다. 이들은 같은 규칙을 준수하는 객체에 의해 구현될 수 있다.

## 이터레이션 프로토콜(Iteration protocol)

![이터레이션 프로토콜(Iteration protocol)](./asset/iteration-protocol.png "이터레이션 프로토콜(Iteration protocol)")

# Iterable (이터러블)

반복 가능한 객체 (iterable object)는 for...of 구문과 함께 ES2015에서 도입되었습니다. 반복 가능한 객체를 다른 객체와 구분짓는 특징은, 객체의 `Symbol.iterator` 속성에 **특별한 형태의 함수**가 들어있는 여부로 확인 할 수 있습니다.

```js
// iterable 객체를 만들어내는 생성자인 String
const str = "hello";
str[Symbol.iterator]; // [Function]

// Num
const num = 2;
num[Symbol.iterator];
// undefined
```

객체의 `Sysmbol.iterator` 속성에 특정 형태의 함수가 들어있다면, 이를 반복 가능한 객체 혹은 줄여서 **iterable**이라 부르고, **해당 객체는 iterable protocol을 만족한다**라고 말합니다. 이런 객체들에 대해서 ES2015애서 추가된 다양한 기능들을 사용할 수있습니다.

✏️내장된 생성자 중 iterable 객체를 만들어내는 생성자에는 아래와 같은 것들이 있습니다.

- String
- Array
- TypedArry
- Map
- Set

즉, **Iterable** 순회가능한 객체로써 `[Symbol.iterator]` 메소드를 구현하고 있고, iterator 객체를 반환하는 객체를 뜻합니다. 이런 스펙을 iterable protocol 이라고 합니다.

## 1. Iterable의 사용

어떤 객체가 Iterable이라면, 그 객체에 대해서 아래의 기능들을 사용할 수 있습니다.

- for...of 루프
- spread 연산자(...)
- 분해대입
- 기타 iterable을 인수로 받는 함수

**즉, 문자열에 대해서도 위기능들을 사용할 수 있습니다.** 아래의 코드를 실해하고 그 결과를 직접 확인해보세요.

```js
// `for...of`
for (let c of "hello") {
  console.log(c);
}

// spread 연산자
const characters = [..."hello"];
//[ 'h', 'e', 'l', 'l', 'o' ]

// 분해대입
const [c1, c2] = "hello";
console.log(c1); // h

// `Array.from`은 iterable 혹은 array-like 객체를 인수로 받습니다.
Array.from("hello");

// split 방법
const characters1 = "hello".split("");
```

---

왜 그냥 for문은 되지 않고 for...of은 무엇이길래 될까?

🔖 `for...of` 구문
ES2015가 나오기 이전까지는 `for`구문이 배열을 순회하는 데에도 많이 사용되었습니다. 하지만 근래에는 배열의 `forEach`메소드나 `for..of`구문이 더 많이 쓰이는 편입니다.

```js
const arr = [1, 2, 3, 4, 5];

for (let item of arr) {
  console.log(`현재 요소는 ${item} 입니다.`);
}
// 현재 요소는 1 입니다.
// 현재 요소는 2 입니다.
// 현재 요소는 3 입니다.
// 현재 요소는 4 입니다.
// 현재 요소는 5 입니다.
```

---

## 2. Generator 함수

그러면 우리가 직접 iterable인 객체를 만들 수는 없을까요? 결론부터 말하면, iterable protocol을 구현하기만 하면 **어떤 객체든 iterable**이 될 수 있습니다.

Iterable을 구현하는 가장 쉬운 방법은 ES2015에 도입된 **generator함수**를 사용하는 것입니다.

Generator 함수는 **iterable 객체를 반환하는 특별한 형태의 함수**입니다.

아래와 같은 문법을 통해 generator 함수를 정의할 수 있습니다.

```js
// generator 함수 선언하기
function* gen1() {
  //...
}

// 표현식으로 사용하기
const gen2 = function*() {
  //...
};

// 메소드 문법으로 사용하기
const obj = {
  *gen3() {
    //...
  }
};
```

---

🔖 함수를 정의하는 방법은 **함수 선언**과 **함수 표현식** 2가지가 있다.

```js
function funcName() {..} // 함수 선언

const funcName = function() {..} // 함수 표현식
```

함수 선언으로 정의된 함수는 **함수 선언 끌어올림(hoisting)**이 발생하며, 함수 실행 코드가 선언보다 먼저 있어도 정상적으로 동작한다.

---

Generator 함수를 호출하면 객체가 생성되는데, 이 객체는 Iterable protocol을 만족합니다. 즉, `Symbol.iterator` 속성을 갖고 있습니다.

```js
function* gen1() {
  //...
}

// `gen1`를 호출하면 iterable이 반환됩니다.
const iterable = gen1();

iterable[Symbol.iterator]; // [Function]
```

Generator 함수 안에 `yield` 라는 특별한 키워드를 사용할 수 있습니다. Generator 함수 안에서 `yield` 키워드는 `return`과 유사한 역활을 하며, iterable의 기능을 사용할 때 **`yield` 키워드 뒤에 있는 값들을 순서대로 넘겨줍니다.**

```js
function* numberGen() {
  yield 1;
  yield 2;
  yield 3;
}

// 1, 2, 3이 순서대로 출력됩니다.
for (let n of numberGen()) {
  console.log(n);
}
```

`yield*`표현식을 사용하면, 다른 generator 함수에서 넘겨준 값을 대신 넘겨줄 수도 있습니다.

```js
function* numberGen() {
  yield 1;
  yield 2;
  yield 3;
}

function* numberGen2() {
  yield* numberGen();
  yield* numberGen();
}

// 1, 2, 3, 1, 2, 3이 순서대로 출력됩니다.
for (let n of numberGen2()) {
  console.log(n);
}
```

`yield` 키워드를 제외하면, generator 함수 내부의 동작 방식은 일반적인 함수와 별반 다르지 않습니다. 즉, 다른 함수에서 할 수 있는 일이라면 generator 함수 안에서도 모두 할 수있습니다.

```js
// 등차수열 생성하기
function* range(start = 0, end = Infinity, step = 1) {
  for (let i = start; i < end; i += step) {
    yield i;
  }
}

// 피보나치 수열 생성하기
function* fibonacci(count = Infinity) {
  let x = 1;
  let y = 1;
  for (let i = 0; i < count; i++) {
    yield x;
    [x, y] = [y, x + y];
  }
}

// 하나의 항목을 계속 넘겨주기
function* repeat(item, count = Infinity) {
  for (let i = 0; i < count; i++) {
    yield item;
  }
}

// 여러 요소를 반복해서 넘겨주기
function* repeatMany(array) {
  while (true) {
    for (let item of array) {
      yield item;
    }
  }
}
```

Generator 함수를 사용할 때 주의할 점이 있습니다.

- Generator 함수로 부터 생성된 iterable은 한 번만 사용될 수 있씁니다.
- Generator 함수 내부에서 정의된 일반 함수에서는 `yield`키워트를 사용할 수 없습니다.

```js
// Generator 함수로부터 생성된 iterable은 한 번만 사용될 수 있습니다.
function* gen() {
  yield 1;
  yield 2;
  yield 3;
}

const iter = gen();

for (let n of iter) {
  // 잘 출력됩니다.
  console.log(n);
}
for (let n of iter) {
  // `iter`는 한 번 사용되었으므로, 이 코드는 실행되지 않습니다.
  console.log(n);
}
```

```js
// Generator 함수 내부에서 정의된 일반 함수에서는 `yield` 키워드를 사용할 수 없습니다.
function* gen2() {
  // 아예 문법 오류가 납니다. (Unexpected token)
  function fakeGen() {
    yield 1;
    yield 2;
    yield 3;
  }
  fakeGen();
}
```

## 3. Iterator Protocol

이제 iterable의 동작 원리를 살혀보겠습니다. **(iterable과 iterator를 잘 구분하세요)**

앞에서 'iterable 객체는 iterable protocol을 만족한다. 즉, `Symbol.iterator`속성에 **특별한 형태의 함수가 저장되어 있다**'고 했습니다.

Iterable protocol(이터러블 프로토콜)을 만족하려면, `Symbol.iterator`속성에 저장되어 있는 함수는 itertor(이터레이터)객체를 반환해야 합니다.

✏️Iterator 객체는 아래의 특별한 조건을 만족하는 객체입니다.

- Iterator는 `next`라는 메소드를 갖습니다.
- `next` 메소드는 다음 두 속성을 갖는 객체를 반환해야 합니다.
  - `done` - 반복이 모두 끝났는지 나탸냅니다.
  - `value` - 현재 순서의 값을 나타냅니다.

위 조건을 **Iterator protocol**이라고 합니다.

```js
// 문자열은 iterable이므로 이로부터 iterator를 생성할 수 있습니다.
const strIterator = "go"[Symbol.iterator]();
strIterator.next(); // { value: 'g', done: false }
strIterator.next(); // { value: 'o', done: false }
strIterator.next(); // { value: undefined, done: true }
strIterator.next(); // { value: undefined, done: true }

// generator 함수로부터 생성된 객체 역시 iterable이므로 이로부터 iterator를 생성할 수 있습니다.
function* gen() {
  yield 1;
  yield 2;
}
const genIterator = gen()[Symbol.iterator]();
genIterator.next(); // { value: 1, done: false }
genIterator.next(); // { value: 2, done: false }
genIterator.next(); // { value: undefined, done: true }
genIterator.next(); // { value: undefined, done: true }
```

iterable 만들기. 앞에 예저에 있었던 `range` 함수를 generator 함수를 사용하지 않고 똑같이 구현

```js
function range(start = 0, end = Infinity, step = 1) {
  // `range` 함수는 iterable을 반환합니다.
  return {
    currentValue: start,
    [Symbol.iterator]() {
      // iterable의 `Symbol.iterator` 메소드는 iterator를 반환해야 합니다.
      return {
        next: () => {
          if (this.currentValue < end) {
            const value = this.currentValue;
            this.currentValue += step;
            return {
              done: false,
              value
            };
          } else {
            return {
              done: true
            };
          }
        }
      };
    }
  };
}
```

Generator 함수를 사용했을 때보다 훨씬 복잡합니다. 이 떄문에 iterator protocol을 직접 구현하는 대신 generator함수를 사용하는 경우가 많습니다. 다만, `next` 메소드를 사용하면 iterable을 세부적으로 제어할 수 있으므로, iterator 대해서 알아둘 필요가 있습니다.

## 4. Generator와 Iterator

Generator 함수로부터 만들어진 객체는 일반적인 iterable처럼 쓸 수 있지만, iterator와 관련된 특별한 성질을 갖고 있습니다.

첫번째로, generator 함수로부터 만들어진 객체는 **iterable protocol과 iterator protocol을 동시에 만족합니다.**

```js
function* gen() {
  // ...
}

const genObj = gen();
genObj[Symbol.iterator]().next === genObj.next; // true
```

즉, `Symbol.iterator`를 통해 iterator를 생성하지 않고도 바로 `next`를 호출할 수 있습니다.

```js
function* gen() {
  yield 1;
  yield 2;
  yield 3;
}

const iter = gen();

iter.next(); // { value: 1, done: false }
iter.next(); // { value: 2, done: false }
iter.next(); // { value: 3, done: false }
iter.next(); // { value: undefined, done: true }
```

두번째로, generator 함수 안에서 `return` 키워드를 사용하면 반복이 바로 끝나면서 `next` 메소드에서 반환되는 객체의 속성에 앞의 반환값이 저장됩니다. 다만, `return`을 통해 반환된 값이 반복 절차에 포함되지는 않습니다.

```js
function* gen() {
  yield 1;
  return 2; // generator 함수는 여기서 종료됩니다.
  yield 3;
}

const iter = gen();

iter.next(); // { value: 1, done: false }
iter.next(); // { value: 2, done: true }
iter.next(); // { value: undefined, done: true }

// `1`만 출력됩니다.
for (let v of gen()) {
  console.log(v);
}
```

세 번째로, generator 함수로부터 생성된 객체의 `next` 메소드에 인수를 주어서 호출하면, generator 함수가 멈췄던 부분의 `yield` 표현식의 결과값은 앞에서 받은 인수가 됩니다.

```js
function* gen() {
  const received = yield 1;
  console.log(received);
}

const iter = gen();
iter.next(); // { value: 1, done: false }

// 'hello'가 출력됩니다.
iter.next("hello"); // { value: undefined, done: true }
```

Generator 함수의 이런 성질은 비동기 프로그래밍을 위해 활용되기도 합니다. 이에 대한 자세한 내용은 **비동기 프로그램밍**에서 다룹니다.

# 참고할 링크

[MDN for...of](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...of)
[ES6: Iterable, Iterator](https://blog.qodot.me/post/es6-iterable-iterator/)
[MDN Generator 함수](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/function*)
[이터레이션 프로토콜(iteration protocol)과 for-of 루프](https://poiemaweb.com/es6-iteration-for-of)

# 면접 질문

1. Iterable과 Iterator이 무엇인가?
1. Generator함수에 대해 설명하세요
