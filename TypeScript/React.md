## CSSProperties

스타일 객체로 나열. `CSSProperties`에는 문자열이 아닌 특정 문자열이 필요하므로 작업중인 객체의 종류를 typescript에 알려 주어야하므로 그에 따라 처리됩니다.

```js
const buttonStyle: CSSProperties = {
  background: `${Colors.redColor}`,
  border: "0",
  padding: "0 2rem",
  fontSize: "1.4rem",
  fontWeight: 500,
  lineHeight: "3rem",
  verticalAlign: "baseline",
  height: "3rem"
};

<Button onClick={() => setParcelModal(row)} style={buttonStyle}>

```

## ChangeEvent

`React.FormEventHandler<HTMLInputElement>`설명 `handleChange`합니다. 이 경우 Typescript `event`매개 변수를 자동으로 인식

```js
  const handleChange = (
    e: ChangeEvent<HTMLSelectElement | HTMLInputElement>
  ) => {
    let value: string | number = e.target.value;
    if (e.target.name === "shopID") value = Number(value);
    if (e.target.name === "id") value = Number(value);
```

## HTMLAttributes

```js
interface InputProps extends HTMLAttributes<HTMLInputElement> {
  value?: string;
  icon?: string;
  type?: string;
  focusIcon?: string;
  name?: string;
  readOnly?: boolean;
  placeholder?: string;
  style?: CSSProperties;
  onChange?: (e: ChangeEvent<HTMLInputElement>) => void;
}
```
