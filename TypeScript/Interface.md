## Interface

값이 가지는 형태에 초점을 맞추는 타입-체킹을 한다는 것입니다.
이것은 떄떄로 "덕 타이핑(duck typeing)" 또는 "구조적 하위 유형화(structural subtyping)"라고도 합니다.
TypeScript 에서는 인터페이스가 이러한 타입의 이름을 지정하는 역할을 하며 코드 내에서 계약을 정의하고 프로젝트 외부에서 코드를 사용하는 계약을 정의하는 강력한 방법입니다.

### First Interface

```js
function printLabel(labelledObj: { label: string }) {
  console.log(labelledObj.label);
}

let myObj = { size: 10, label: "Size 10 Object" };
printLabel(myObj);

//Size 10 Object
```

타입-체커는 `printLabel`에 대한 호출을 확인합니다.
`printLabel`함수에는 객체를 전달하는데 필요한 단일 매개변수가 있으면 이는 문자역 타입 `label` 프로퍼티를 가집니다.
실제로 객체는 이보다 더 많은 프로퍼티를 가지고 있지만 컴파일러는 필요한 속성이 최소한 있고 필요한 타입과 일치하는지먼 검사합니다.

#### Interface

인터페이스를 사용하여 문자열 타입인 `label`프로퍼티를 가져야 한다는 요구사항을 설명하는 동일한 예제를 가시 작성할 수 있습니다.

```js
interface LabelledValue {
  label: string;
}

function printLabel(labelledObj: LabelledValue) {
  console.log(labelledObj.label);
}

let myObj = { size: 10, label: "Size 10 Object" };
printLabel(myObj);
```

인터페이스 `LabelledValue` 이전 예저의 요구 사항을 설명하는데 사용할 수 있는 이름입니다.
여전히 `label`이라는 문자열 타입의 단일 프로퍼티가 있습니다.
`printLabel`에 전달하는 객체가 다른 언어처럼 이 인터페이스를 구현한다고 명시적으로 말할 필요가 없었습니다. 여기서는 중요한 형태일 뿐입니다. 함수로 전달되는 객체가 나열된 요구 사항을 충족하는 경우 허용됩니다.

타입-체커에서는 이러한 프로퍼티가 순서대로 제공될 것을 요구하지 않으며 다만 인터페이스에 필요한 속성이 있고 필요한 타입만 필요하다는 점을 지적하는 것이 중요합니다.

### 선택적 프로퍼티

인터페이스의 모든 프로퍼티가 필수로 필요할 수는 없습ㄴ디ㅏ.
어떤 것들은 특정한 조건 하에 존재하거나 아예 존재하지 않을 수도 있습니다.
