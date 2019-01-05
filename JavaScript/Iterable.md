#Iterable

반복 가능한 객체 (iterable object)는 for...of 구문과 함께 ES2015에서 도입되었습니다. 반복 가능한 객체를 다른 객체와 구분짓는 특징은, 객체의 `Symbol.iterator` 속성에 **특별한 형태의 함수**가 들어있는 여부로 확인 할 수 있습니다.

```js
// iterable 객체를 만들어내는 생성자
const str = "hello";
str[Symbol.iterator]; // [Function]
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

// 분해대입
const [c1, c2] = "hello";

// `Array.from`은 iterable 혹은 array-like 객체를 인수로 받습니다.
Array.from("hello");

// split 방법
const characters1 = "hello".split("");
```

---

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

Generator 함수를 호출하면 객체가 생성되는데, 이 객체는 Iterable protocol을 만족합니다. 즉, `Symbol.iterator`

# 참고할 링크

[MDN for...of](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Statements/for...of)
[ES6: Iterable, Iterator](https://blog.qodot.me/post/es6-iterable-iterator/)
