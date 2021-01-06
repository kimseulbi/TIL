## Function 함수

```js
let z = 100;

function addToZ(x, y) {
  return x + y + z;
}

addToZ(1, 2);

// 함수는 함수 본문 외부의 변수를 참조할 수 있습니다. 이렇게 할 때 이러한 변수들을 capture 라고 말합니다.
```

### 함수 작성

```js
function add(x: number, y: number): number {
  return x + y;
}

let myAdd = function(x: number, y: number): number {
  return x * y;
};

add(1, 2); //3
myAdd(1, 2); //2
```

각 매개변수에 타입을 추가 한 다음 함수 자체에 타입을 추가하여 반환 타입을 추가할 수 있습니다.
TypeScript는 리턴문을 보고 반환 타입을 파악할 수 있기 때문에 대부분 선택적으로 반환타입을 생략할 수 있습니다.

### 함수 타입 작성하기

```js
let myAdd: (x: number, y: number) => number = function(
  x: number,
  y: number
): number {
  return x + y;
};
```

함수의 타입은 두개의 파트로 나뉩니다. 인수의 타입과 반환 타아ㅣㅂ. 전체 함수 타입을 작성할 때 두 파트가 모두 필요합나다.
매개변수 타입과 같이 매개변수 목록을 기록하여 각 매개변수에 이름과 타입을 지정합니다.

```js
let myAdd: (baseValue: number, increment: number) => number = function(
  x: number,
  y: number
): number {
  return x + y;
};
```

매개변수 타입이 정렬되어 있는 한 함수의 타입에 매개변수를 제공하는 이름에 관계 없이 매개변수 타입이 유효한 타입으로 간주됩니다.

두 번째 파트는 반환 타입입니다.
매개변수와 반환 타입 사이에 화살표 함수(=>)를 사용하여 반환 타입을 명확하게 합니다.
앞서 언급한 것처럼 이것은 함수 타입의 필수적인 부분이므로 함수가 값을 반환하지 않는 경우에는 반환 값을 남겨 두지 않고 `void`를 사용합니다.

주의사항, 매개변수와 반환 타입만 함수 타입을 구성합니다.
캡처된 변수는 타입에 반영되지 않습니다.
실제로 갭처된 변수는 함수의 "숨겨진 상태"의 일부이며 해당 API를 구성하지 않습니다.

### 선택적 매개변수와 기본 매개변수

JavaScript에서 모든 매개변수는 선택 사항이며 매개변수를 원하는 대로 사용하지 않을 수 있습니다.
그렇게 되면 그 매개변수들의 값은 `undefined`입니다. TypeScript에서 선택적인 매개변수를 사용하려면 선택적으로 사용하려는 매개변수의 끝에 `?`을 추가하세요.

```js
// 선택적 매개변수
function buildName(firstName: string, lastName?: string) {
  if (lastName) return firstName + " " + lastName;
  else return firstName;
}

let result1 = buildName("Bob"); // Bob
let result2 = buildName("Bob", "Adams", "Sr."); // 오류, 너무 많은 매개변수
let result3 = buildName("Bob", "Adams"); // Bob Adams
```

모든 선택적 매개변수는 필수 매개변수를 따라와야 합니다.
last name 대신 first name을 선택적 매개변수로 만들고 싶다면 함수의 매개변수 순서를 변경해야합니다.
즉 목록의 first name을 마지막에 넣어야합니다.

TypeScipt에서 사용자가 매개변수를 제공하지 않거나 사용자가 대신`undefined`를 전달하더라도 매개변수에 할당되는 값을 설정할 수 있습니다.

```js
// 매개변수 기본값 설정
function buildName(firstName: string, lastName = "Smith") {
  return firstName + " " + lastName;
}

let result1 = buildName("Bob"); // 올바르게 작동하며 "Bob Smith"를 반환합니다
let result2 = buildName("Bob", undefined); // 여전히 작동하며 "Bob Smith"를 반환합니다.
let result3 = buildName("Bob", "Adams", "Sr."); // 오류, 너무 많은 매개변수
let result4 = buildName("Bob", "Adams"); // 아, 딱 맞습니다
```

필수 매개변수의 뒤에 오는 기본 매개변수는 선택적 매개변수로 취급되어 함수를 호출할 때 선태적 매개변수처럼 생략할 수 있습니다.
이것은 선택적 매개변수와 후행 기본 매개변수가 해당 타입의 공통점을 공유한다는 것을 의미하므로 둘 다 그리고 `(firstName: string, lastName?: string) => string` 동일한 타입을 공유합니다.

매개변수에 기본값 설정은 마지막 매개변수만 가능합니다.

### 나머지 매개변수

필수 매개변수와 선택적 매개변수 그리고 기본 매개변수 모두 공통점이 하나 있습니다: 한 번에 하나의 매개변수에 대해 이야기합니다.
때로는 여러 매개변수를 그룹으로 사용하거나 함수가 마지막으로 가져올 매개변수의 수를 모를 수 있습니다.

```js
function buildName(firstName: string, ...restOfName: string[]) {
  return firstName + " " + restOfName.join(" ");
}

let employeeName = buildName("Joseph", "Samuel", "Lucas", "MacKinzie");
//Joseph Samuel Lucas MacKinzie
```

나머지 매개변수는 무한적인 수의 선택적 매개변수로 처리됩니다.
Rest 매개변수에 인수를 전달할 때는 원하는 만큼 사용할 수 있으면 심지어 통과할 수 없습니다. 컴파일러는 줄임표(...)다음에 전달된 인수들을 배열을 작성하여 함수에서 사용할 수 있습니다.

줄임표(...)는 나머지 매개변수가 있는 함수의 타입에도 사용됩니다.

```js
function buildName(firstName: string, ...restOfName: string[]) {
  return firstName + " " + restOfName.join(" ");
}

let buildNameFun: (fname: string, ...rest: string[]) => string = buildName;
```
