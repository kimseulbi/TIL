# ES5 VS ES2015

## ECMAScript 즉 ES는 무엇?

> ECMAScript는 스크립트 언어의 표준이며 JavaScript 언어는 ECMAScript 표준을 기반으로 합니다.

ES는 자바스크립트를 이루는 코어스크립트 언어로써, 다양한 환경에서 운용될 수 있게 확장성을 갖고 있기 때문에 사용처가 웹환경으로 국한되어있지는 않습니다. 즉, 자바스크립트를 웹브라우저에서 들어갈 수 있도록 `BOM`과 `COM`을 함께 사용하는 확장성이 되었습니다. 이러한 확장성들은 ES버전에 따른 문법과 기능의 확장을 가능하게 합니다.

```
자바스크립트= ECMAScript + BOM + DOM
```

## ES의 버전관리는 어떻게 되는거지?

```
ES3 -> ES5 -> ES2015 -> ES2016
```

ES5의 다음부터 해당 버전이 공개된 연도를 버전 번호로 사용합니다. 즉, ES5의 다음 버전의 이름은 ES6이 아니라 **ES2015** 입니다.

## ES05 (2009)

ES4는 너무 시대의 흐름을 앞서갔는지 거절되고, 이후 점진적인 개성을 목표로 ES5가 나왔다. 아무리 그래도 10년만에 버전업....😩

- 배열과 관련하여 편리한 메소드들이 다수 생겼다. `forEach` `map` `reduce` `filter` `some` `every`와 같은 순환 메소드들이 생겼다. 이 메소드들은 개발 시 불필요한 중복 코드를 줄어주어서 가독성은 높이고 버그율은 낮추는 효과줌~
- 객체는 프로퍼티에 대한 설정을 할 수 있게 되었다. 객체를 생성, 수정, 복사하고 표준 메소드 `Object.Create()` `Object.defineProperty()` `Object.freeze()` `Object.assign()` 등 과 `getter`, `setter` 등이 추가 되었으며, `Object.keys()` 메소드를 이용하면 `for in`메소드도 대체할 수 있게 되었다.
- `strict` 엄격모드 문법을 좀 더 낀깐하게 체크 하는 모드로 개발자가 인지할 수 있는 범위 안에서 개발할 수 있도록 사용하기 위해 등장
- `bind()` 메소드 this를 바인딩 시켜주는 메소드, 메소드의 인수로 넘겨준 값이 `this`가 되는 새로운 함수를 반환

[ES5의 기능추가 목록 및 브라우저 호환성 테이블](http://kangax.github.io/compat-table/es5/)

## ES2015 (2015)

아직까지 많은 브라우저가 ES2015을 온전하게 지원하지 않는 상태라 [Babel](https://babeljs.io/)이나 [Traceur](https://github.com/google/traceur-compiler)와 같은 트랜스파일러를 사용해 하위 버전인 ECMAScript 5(이하 ES5)로 변환하는 과정을 거쳐야 ES6을 사용할 수 있다.

**대표적인 10가지**

- 기본 매개 변수 (Default Parameters)
- 템플릿 리터럴 (Template Literals)
- 멀티 라인 문자열 (Multi-line Strings)
- 분해대입 (Destructuring Assignment)
- 향상된 객체 리터럴 (Enhanced Object Literals)
- 화살표 함수 (Arrow Functions)
- Promises
- 블록 범위 생성자 let 및 cosnt
- 클래스 (Classes)
- 모듈 (Modules)

[ECMAScript 6 Features 추가된 기능](https://seokjun.kim/ecmascript-6-features/)

[ES2015의 기능추가 목록 및 브라우저 호환성 테이블](http://kangax.github.io/compat-table/es6/)

## ES2016

ES2015이랑 큰 변화는 없었다. 비교하자면 조금 바뀜~

- `제곱 연산자(**)` 등장
- `Array.includes`배열에 해당 요소가 존재하는지 확인하는 메소드 등장

## ES2017

ES2017에서는 Promise 급의 중대한 변환인 `async` `await`등이 발표되었습니다.

- async
- await
- 객체의 좀더 심화된 메소드가 등장했습니다. Object.keys()에 대응되는 메소드 인 `Object.values()`Object.keys()와 Object.values()를 합쳐 놓은 `Object.entries()`, Object.getOwnPropertyDescriptor의 복수형태인 `Object.getOwnPropertDescriptors()`로써 상속받지 않은 속성들의 설명만 보여줍니다.
- 문자열 단순 편의기능이 추가되었습니다. 문자열 앞부분에 공백을 넣어 자리수를 맞춰주는 `String.padStart()`, 문자열 뒷부분에 동백을 넣어 자리수를 맞춰주는 `String.padEnd()`
- 매개변수 마지막에 콤마를 붙이는걸 허용

## ES5 ES2015 10가지 비교 (완전복습인가?)

### 1. 기본 매개변수

```js
function link(url) {
  if (url === undefined) {
    url = "https://www.naver.com";
  }
  console.log(url);
}
link(); // https://www.naver.com
link("www"); // www
link(undefined); //  https://www.naver.com
```

함수에 넘겨주는 인자값에 대한 default 처리를 위해 위와 같이 처리 했다면 ES6에서는 아래와 같은 간단한 처리를 하였다.🤩

```js
// https://www.naver.com가 `url` 매개변수의 기본값이 됩니다.
function link(url = "https://www.naver.com") {
  console.log(`${url}`);
}
link(); // https://www.naver.com
link("www"); // www
link(undefined); //  https://www.naver.com
```

```
🏷 매개변수: function add(x, y)라는 함수에 x,y를 매개변수입니다. 함수 호출 시마다 인수가 매개변수에 대입
```

### 2. 템플릿 리터럴

ES5에서는 아래와 같은 문자열을 처리

```js
var name = "your name is" + lastName;
```

하지만 ES2015에서는 템플릿 리터럴을 제공하므로 ` (back-ticked)문자열안에 \${name} 이라는 새로운 구문을 사용해서 아래와 같이 간단히 처리할 수 있습니다.

```js
let name = `your name is ${lastName}`;
```

### 3. 멀티 라인 문자열

ES5에서는 멀티라인 문자열을 처리하기 위해 아래와 같은 방법들을 사용해야 했다.

```js
var roadPoem =
  "Then took the other, as just as fair,\n\t" +
  "And having perhaps the better claim\n\t" +
  "Because it was grassy and wanted wear,\n\t" +
  "Though as for that the passing there\n\t" +
  "Had worn them really about the same,\n\t";

var fourAgreements =
  "You have the right to be you.\n\
    You can only be you when you do your best.";
```

하지만 ES2015에서는 `(back-ticked) 문자열을 이용해서 아래와 같은 간단히 처리할 수 있다.

```js
let roadPoem = `Then took the other, as just as fair,
    And having perhaps the better claim
    Because it was grassy and wanted wear,
    Though as for that the passing there
    Had worn them really about the same,`;

let fourAgreements = `You have the right to be you.
    You can only be you when you do your best.`;
```

### 4. 분해대입

ES5에서는 구조화된 데이터를 변수로 받기 위해 아래와 같이 처리해야한다.

```js
var array = [1, 2, 3];
var a = array[0];
var b = array[array.length - 1];

console.log(a); // 1
console.log(b); // 3
```

하지만 ES2015에서 배열과 객체 안에 들어있는 값을 쉽게 추출해낼 수 있는 문법이 추가되었습니다.

```js
// 배열
const [a, , c] = [1, 2, 3, 4];

console.log(a, c); // 1 3

// 객체
const { a, b } = { a: 1, b: 2 };

console.log(a, b); // 1 2
```

### 5. 향상된 객체 리터럴 (다시 읽어볼 필요가 있음...)

ES5에서는 아래와 같이 JSON을 사용해서 객체 리터럴을 만들수 있습니다.

```js
var serviceBase = { port: 3000, url: "azat.co" },
  getAccounts = function() {
    return [1, 2, 3];
  };

var accountServiceES5 = {
  port: serviceBase.port,
  url: serviceBase.url,
  getAccounts: getAccounts,
  toString: function() {
    return JSON.stringify(this.valueOf());
  },
  getUrl: function() {
    return "http://" + this.url + ":" + this.port;
  },
  valueOf_1_2_3: getAccounts()
};
```

위 예시와 달리 serviceBase를 확장하길 원한다면 Object.create 로 프로토타입화하여 상속 받을 수 있다.

```js
let accountServiceES5ObjectCreate = {
  getAccounts: getAccounts,
  toString: function() {
    return JSON.stringify(this.valueOf());
  },
  getUrl: function() {
    return "http://" + this.url + ":" + this.port;
  },
  valueOf_1_2_3: getAccounts()
};
accountServiceES5ObjectCreate.__proto__ = Object.create(serviceBase);
```

accountServiceES5ObjectCreate와 accountServiceES5는 동일하게 사용할 수 있으나 다른 구조를 가진다. accountServiceES5ObjectCreate는 accountServiceES5와 다르게 `__proto__` 에 `port` 와 `url` 속성을 가진 객체를 담고 있다.

ES6에서는 아래와 같이 처리할 수 있다.

```js
var serviceBase = { port: 3000, url: "azat.co" },
  getAccounts = function() {
    return [1, 2, 3];
  };
var accountService = {
  __proto__: serviceBase,
  getAccounts,
  toString() {
    return JSON.stringify(super.valueOf());
  },
  getUrl() {
    return "http://" + this.url + ":" + this.port;
  },
  ["valueOf_" + getAccounts().join("_")]: getAccounts()
};
```

위 예시에 대해 ES5와의 차이를 요약하면 아래와 같다.

- `__proto__`속성을 사용해서 바로 프로토타입을 설정할 수 있다.
- `getAccounts: getAccounts`, 대신 `getAccounts, 를 사용할 수 있다 (변수명으로 속성 이름을 지정).
- `[ 'valueOf_' + getAccounts().join('_') ]` 와 같이 동적으로 속성 이름을 정의할 수 있다.

### 6. 화살표 함수

화살표 기능은 Javascript에 많은 명확성과 코드 감소를 해줍니다. 함수를 정의 하는 방법 알아봅시다.

ES5버전

```js
function greetings(name) {
  return "hello" + name;
}
```

ES2015에서는 아래와 같은 방식으로 정의할 수 있습니다.

```js
const greetings = name => {
  return `hello ${name}`;
};
```

`function` 함수를 정의 하기 위해 키워드를 사용하지 않아도 됩니다. 좀 더 코드를 축소 할수 있습니다. `return`키워드를 쓰지 않고 중괄호 안에 함수을 작성 하지 않아도 ES2015가 알아서 자동으로 반환 해준다고 한다.

```js
onst greetings = name =>`hello $ {name}`;
```

---

나는 공부 다시해야될꺼같아서...
🏷 [helloJS 화살표함수](https://helloworldjavascript.net/pages/230-function-in-depth.html)

---

### 7. Promises

ES5에 콜백의 문제를 해결하기 위해 나왔던 라이브러리가 ES2015에 이르러 Promise 언어 자체가 포함이 되었습니다.

`setTimeout`을 이용한 지연된 비동기 실행에 대해 설명 하겠음~~~
ES5에서 지연된 비동기 실랭에 대한 예시입니다.

```js
setTimeout(function() {
  console.log("Yay!");
}, 1000);
```

아래는 ES2015에서 Promises를 사용해서 재작성한것 입니다.
Promises사용이 복잡한 비동기 데이터를 흐름을 다룰때 좋고 `then`메소드 메소드는 Promise 객체를 반환하므로, 콜백을 중첩하지 않고도 비동기 작업을 연이어 할 수 있습니다.
비동기 작업이라는 동작 자체를 값으로 다룰 수 있게 됩니다.

```js
var wait1000 = new Promise(function(resolve, reject) {
  setTimeout(resolve, 1000);
}).then(function() {
  console.log("Yay!");
});
```

---

나는 공부 다시해야될꺼같아서...
🏷 [helloJS Promise](https://helloworldjavascript.net/pages/285-async.html)

---

### 8. 블록 스코프 let과 const

`let`과 `const`는 같은 이름을 갖는 변수의 재선언을 하지 않으며 둘 다 블록 스코프를 갖는다.

```js
function calculateTotalAmount(vip) {
  var amount = 0;
  if (vip) {
    var amount = 1;
  }
  {
    // more crazy blocks!
    var amount = 100;
    {
      var amount = 1000;
    }
  }
  return amount;
}
calculateTotalAmount(true); //1000
```

`var`는 전역 또는 함수 내부로 유효 범위를 갖기 때문에 예시에 사용된 함수 내부의 "{}"들은 아무런 역활을 하지 못하기때문에 결과값이 1000
`var`는 함수스코프를 갖고 있기 때문에 `var`변수는 해당 블록 바깥에서도 유효합니다.

```js
function calculateTotalAmount(vip) {
  let amount = 0; // probably should also be let, but you can mix var and let
  if (vip) {
    let amount = 1; // first amount is still 0
  }
  {
    // more crazy blocks!
    let amount = 100; // first amount is still 0
    {
      let amount = 1000; // first amount is still 0
    }
  }
  return amount;
}
calculateTotalAmount(true); //0
```

`let` 으로 선언된 변수는 "{}" 블록 내부로 유효 범위가 한정되므로 100, 1000으로 할당된 변수는 해당 블록 내부에서만 유효함. `const`는 상수를 선언하는 것으로 여러번 선언될 수 없지만 let과 같이 블록 내부로 유효 범위가 한정되므로 아래의 예시는 오류가 발생하지 않는다.

```js
function calculateTotalAmount(vip) {
  const amount = 0;
  if (vip) {
    const amount = 1;
  }
  {
    // more crazy blocks!
    const amount = 100;
    {
      const amount = 1000;
    }
  }
  return amount;
}
calculateTotalAmount(true); //0
```

### 9. 클래스

ES2015에는 `class`키워트가 추가되어 ES5의 prototype 기반 상속보다 명확하게 `class`를 정의할 수 있다.

위 예제를 프로토타입 관점에서 표현해 보면 아래와 같다.

```js
// ES5
var Person = (function() {
  // Constructor
  function Person(name) {
    this._name = name;
  }

  // public method
  Person.prototype.sayHi = function() {
    console.log("Hi! " + this._name);
  };

  // return constructor
  return Person;
})();

var me = new Person("Lee");
me.sayHi(); // Hi! Lee.
```

`get`과 `set`키워드 외에도 `static`키워드를 사용해 static 메소드를 정의하는 것도 가능하다.

```js
class Person {
  constructor(name) {
    this._name = name;
  }

  sayHi() {
    console.log(`Hi! ${this._name}`);
  }
}

const me = new Person("Lee");
me.sayHi(); // Hi! Lee
```

---

나는 공부 다시해야될꺼같아서...
🏷 [poiemaweb class](https://poiemaweb.com/es6-class)

---

### 10. 모듈

ES2015에서 모듈을 공식적으로 제공하기 전까지는 CommonJS, AMD, RequireJS 등의 비공식 모듈 스펙을 사용했습니다. ES2015에서 제공하는 모듈 스펙이랑 달라요!!

ES5에서 CommonJS를 이용해서 모듈을 사용하는 예시는 아래와 같다.

```js
module.exports = {
  port: 3000,
  getAccounts: function() {
    ...
  }
}
```

ES2015의 `import`와 `export`를 사용해서 유사한 가능을 구현 예시다.

```js
export let port = 3000
export function getAccounts(url) {
  ...
}
```

`import`를 사용해서 module.js 모듈을 불러올 수 있다.

```js
import { port, getAccounts } from "module";
console.log(port); // 3000
```

유사하지만 `export`된 모든 변수를 아래와 같은 하나의 구조화된 데이터를 받을 수도 있다.

```js
import * as service from "module";
console.log(service.port); // 3000
```

복습 되었나 ??? 🤯

## ES2015 당장 사용할 수 있는 방법

ES2015는 확정되었지만 아직 모든 브라우저에서 완전하게 지원되지 않는다.
따라서 지금 당장 ES2015 사용하고 싶다면 [Babel](https://babeljs.io/)과 같은 컴파일러를 사용해야한다. Babel은 독립 실행형 도구로 실해하거나 빌드 시스템에서 사용할 수 있다.

# 참고할 링크

[D2 2017년과 이후 JavaScript의 동향](https://d2.naver.com/helloworld/2809766)

[ECMAScript 6 Features 추가된 기능](https://seokjun.kim/ecmascript-6-features/)

[ES5 VS ES6](https://medium.com/recraftrelic/es5-vs-es6-with-example-code-9901fa0136fc)

# 면접 질문

딱히 없어요... 이미 한것들... 😰
