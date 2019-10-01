# 1.0 Layouts with Flexbox in React Native

```js 
import React from 'react';
import { StyleSheet, Text, View } from 'react-native';

export default function App() {
  return (
    <View style={styles.container}>
      <View style={styles.yellowView}>
        <Text>Hello</Text>
      </View>
      <View style={styles.blueView}>
        <Text>Hello</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  yellowView: {
    flex: 1,
    backgroundColor: "yellow",
    alignItems: 'center',
    justifyContent: 'center',
  },
  blueView: {
    flex: 3,
    backgroundColor: "blue",
    alignItems: 'center',
    justifyContent: 'center',
  }
});
```

> `flex: 1` 모든 공간 사용가능 하는 걸 의미

* 리액트 네이티브에 `flexDirection` 기본값은 `column`
* **리액트 네이티브는 `width`, `height`가 필요 없으며 `flex`로 레이아웃코딩을 권장한다.**
* flex는 그냥 자리 경쟁하는 형제들이고, 더 큰 애가 대부분의 자리를 차지한다.
