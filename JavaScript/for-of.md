#ES06 for..of

ES06에서 새로운 요소로 추가된 for..of에 대해 알아봅시다.

배열을 루프로 순회하기 위해 어떤 방법을 사용했나요?

```js
// for문
or (var index = 0; index < myArray.length; index++) {
  console.log(myArray[index]);
}
```

ES05발표 이후에는 `forEach`메소드를 쓸 수 있게 되었습니다.

```js
const arr = [1, 2, 3, 4, 5];

arr.forEach((item, index) => {
  console.log(`배열의 ${index + 1} 번째 요소는 ${item} 입니다.`);
});
```

좀 더 간단한 방법이기는 하지만, 여기에는 사소한 단점이 있습니다. `break`구문을 이용해서 루프를 중단하거나

# 참고할 링크

[for-of 루프 구문](http://hacks.mozilla.or.kr/2015/08/es6-in-depth-iterators-and-the-for-of-loop/)
