# 합성 vs 상속

React는 강력한 합성 모델을 가지고 있기 때문에, 컴포넌트 간에 코드를 재사용해야할 때는 상속 대신 합성을 사용하는 것을 권장합니다.

### 다른 컴포넌트를 담기

컴포넌트에 어떤 자식이 들어올 지 미리 알 수 없는 경우가 있습니다. 이는 `sidebar`나 `dialog` 같은 컴포넌트에서 많이 나타는 패턴입니다.

이러한 경우, `children`이라는 특별한 prop을 통해 자식요소를 그대로 전달하는 방법입니다.

```js
function FancyBorder(props) {
  return (
    <div className={"FancyBorder FancyBorder-" + props.color}>
      {props.children}
    </div>
  );
}
```

다른 컴포넌트에서 JSX를 중첩하여 어떤 자식이든 전달할 수 있습니다.

[Try it on CodePen.](https://codepen.io/gaearon/pen/ozqNOV?editors=0010)

`<FancyBorder>` JSX 태그 안에 있는 것들은 `FancyBorder` 컴포넌트의 `children prop`을 통해 전달됩니다. `FancyBrorder` 는`{props.children}` 를 `<div>`안에 렌더링하므로 전달된 요소들이 최종 출력에 나타납니다.
