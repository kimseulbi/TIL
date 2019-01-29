# SASS

![](https://img1.daumcdn.net/thumb/R1920x0/?fname=http%3A%2F%2Fcfile26.uf.tistory.com%2Fimage%2F217CBF3657E600D61F99FD)

## SASS란?

`SASS(Syntactically Awesome Style Sheet)`라는 단어의 줄임말이며, 한글로 번역하자면 "문장 구성적으로 끝내주는 스타일 시트"라는 의미를 지닙니다.

`SASS`는 문서의 구조를 깔끔하고 구조적으로 기술하는데 사용하는 기술인 css의 상위에 있는 메타언어로, 자바스크립트처럼 특정 속성의 값을 변수로 선언하여 필요한 곳에 선언된 변수를 적용할 수도 있고, 반복되는 코드를 한번의 선언으로 여러 곳에 재사용할 수 있도록 도와주는 일종의 CSS전처리기입니다.

## SASS를 왜 사용할까요???

CSS로 충분한데? 왜 SASS를 사용할까요? 의문이 가죠? 알아봅시다!!!!!! 가즈아~~~~

[Sass, LESS 등을 권장하는 이유 - 심화](https://findawayer.tistory.com/entry/Sass-LESS-%EB%93%B1%EC%9D%84-%EA%B6%8C%EC%9E%A5%ED%95%98%EB%8A%94-%EC%9D%B4%EC%9C%A0)

CSS의 간결한 문법은 배우기 쉬우며 명확하여 프로젝트 초기에는 문제가 없이 보이지만 **프로젝트의 규모가 커지고 수정이 빈번히 발생함에 따라 쉽게 지저분해지고 유지보수도 어려워지는 단점도 가지고 있다.**

이러한 CSS의 태생적 한계를 보완하기 위해 Sass는 다음과 같은 추가 기능과 유용한 도구들을 제공한다.

- 변수의 사용
- 조건문과 반복문
- Import
- Nesting
- Mixin
- Extend/Inheritance

```
이 경우에 SASS가 좋아요!!

* 상당 기간 동안 제품을 제작하고 유지
* 다른 능력과 특기를 소유한 개발자들이 있는 경우
* 여러 명의 다른 개발자들이 있는 경우
* 정기적으로 직원이 충원되는 경우
* 개발자들이 들락날락하는 다수의 코드베이스를 가진 경우
```

### CSS와 Sass 비교

- CSS보다 심플한 표기법으로 **CSS를 구조화**하여 표현할 수 있다.
- 스킬 레벨이 다른 팀원들과의 작업 시 발생할 수 있는 **구문의 수준 차이를 평준화**할 수 있다.
- CSS에는 존재하지 않는 Mixin 등의 강력한 기능을 활용하여 **CSS 유지보수 편의성을 큰 폭으로 향상**시킬 수 있다.

## Install 및 compile

![](https://3.bp.blogspot.com/-b5_ONbOZ6e0/V9ztm1loY2I/AAAAAAAAPGg/-ea_N8QlcnAIDjJek0iRy3IXSrubkaxbwCLcB/s1600/sass-compile.png)

브라우저는 Sass의 문법을 알지 못하기 때문에 Sass(.scss) 파일을 css 파일로 컴파일(트랜스파일링)하여야 한다. 따라서 Sass 환경의 설치가 필요합니다.

sass를 컴파일하는 방법은 여러가지가 있습니다. 그중에서 제알 많이 사용하고 선호 하는 `node-sass`를 보겠습니다~

### 1. node-sass

컴파일속도가 제일 빠르고 Node.js환경에서 작업을 하므로 node 환경에서 libsass를 사용 할 수 있게 해주는 `node-sass`를 사용합니다.

> 🔖 libsass \
> 이는 C언어로 작성된 매우 빠른 Sass compiler 입니다.
> 많은 환경에서 사용될 수 있습니다.

```
// NPM 을 통하여 node-sass 글로벌 설치
$ npm install -g node-sass

# 컴파일하여 현재 디렉토리에 저장
$ node-sass style.scss -o .

# style.scss 파일에 변화가 있을 떄 마다 자동으로 리컴파일
$ node-sass style.scss -w -o .
```

### 2. vscode

#### vscode sass compile 하기 위한 확장프로그램 설치

[Live Sass Compiler](https://marketplace.visualstudio.com/items?itemName=ritwickdey.live-sass)

![](https://github.com/ritwickdey/vscode-live-sass-compiler/raw/master/./images/Screenshot/AnimatedPreview.gif)

#### vscode sass compile 방법

1. test으로 폴더 및 파일 생성을 하세요~~~~

   ![](https://t1.daumcdn.net/cfile/tistory/99063D355B6B99950D)

2. 그럼 화면 아래에 Watsh Sass 클릭하면 compile 완료!

   ![](https://t1.daumcdn.net/cfile/tistory/99315A335B6B9AC10B)

3. 아래 화면은 compile이 완료된 모습이다.
   ![](https://t1.daumcdn.net/cfile/tistory/9953E2335B6B9C930D)

## SASS vs SCSS

Sass는 SASS 표기법(.sass)과 SCSS 표기법(.scss)입니다. 이전 버전에서는 SASS 표기법이 기본 표기법이었으나 Sass 3.0부터 CSS 친화적인 SCSS（Sassy CSS） 표기법이 기본 표기법이 되었습니다.

|             | SCSS     | SASS                                            | CSS    |
| ----------- | -------- | ----------------------------------------------- | ------ |
| 중괄호 {}   | 필요     | 불필요（공백 2문자 들여쓰기가 코드 블록을 의미) | 필요   |
| 세미콜론 ;  | 필요     | 불필요                                          | 필요   |
| : 뒤의 공백 | 불필요   | 필요                                            | 불필요 |
| Mixin       | @mixin   | =                                               | 없음   |
| Include     | @include | +                                               | 없음   |
| 확장자      | .scss    | .sass                                           | .css   |

SASS 표기법은 보다 코딩을 간략화할 수 있는 장점이 있지만 CSS 친화적인 SCSS 표기법를 사용하는 경우가 더 많이 사용합니다.

지금 해볼 설계는 Hugo Giraudel이라는 프로트엔드개발자가 제시하는 방법이에요. 이 방법이 다 맞다고 할 수 없어요.

[SCSS -> CSS](https://www.sassmeister.com/)
[CSS -> SCSS]()

## 문법

[sass 문법이 잘 정리되었어요. 볼까요 ? ](https://heropy.blog/2018/01/31/sass/)

### 주석

Sass(SCSS)는 JavaScript처럼 두 가지 스타일의 주석을 사용합니다.

```scss
// 컴파일되지 않는 주석
/* 컴파일되는 주석 */
```

### 데이터 종류

| 데이터   | 설명                                                        | 예시                                                  |
| -------- | ----------------------------------------------------------- | ----------------------------------------------------- |
| Numbers  | 숫자 (숫자에 단위가 있거나 없습니다.)                       | 1, .82, 20px, 2em…                                    |
| Strings  | 문자 (문자에 따옴표가 있거나 없습니다.)                     | bold, relative, "/images/a.png", "dotum"              |
| Colors   | 색상 표현 (속성값으로 null이 사용되면 컴파일하지 않습니다.) | red, blue, #FFFF00, rgba(255,0,0,.5)                  |
| Booleans | 논리 (**null**이 사용되면 컴퍼일하지 않습니다.)             | true, false                                           |
| Nulls    | 아무것도 없음 (`()`를 붙이거나 붙이지 않습니다.)            | null                                                  |
| Lists    | 공백이나 ,로 구분된 값의 목록 (`()`를 꼭 붙여야 합니다.)    | (apple, orange, banana), Helvetica, Arial, sans-serif |
| Maps     | Lists와 유사하나 값이 Key: Value 형태                       | (apple: a, orange: o, banana: b)                      |

### 중첩

[중첩 실습](https://codesandbox.io/s/7yyzwlnz6j)

상위 선택자의 반복을 피하고 좀 더 편리하게 복잡한 구조를 작성할 수 있습니다.

#### 상위 선택자 참조

중첩 안에서 `&` 키워드는 상위(부모) 선택자를 참조하여 치환합니다.

#### @at-root (중첩 벗어나기)

중첩에서 벗어나고 싶을 때 `@at-root` 키워드를 사용합니다.
중첩 안에서 생성하되 중첩 밖에서 사용해야 경우에 유용합니다.

#### 중첩된 속성

`font-`, `margin-` 등과 같이 동일한 네임 스페이스를 가지는 속성들을 다음과 같이 사용할 수 있습니다.

### 변수

[변수 실습](https://codesandbox.io/s/r7nk90vqr4)

반복적으로 사용되는 값을 변수로 지정할 수 있습니다.
변수 이름 앞에는 항상 `$`를 붙입니다.

```scss
$변수이름: 속성값;
```

#### 변수 유효범위

변수는 사용 가능한 유효범위가 있습니다.
선언된 블록(`{}`) 내에서만 유효범위를 가집니다.

#### 변수 재 할당

변수는 재 할당이 가능합니다.

#### !global (전역 설정)

`!global` 플래그를 사용하면 변수의 유효범위를 전역(Global)로 설정할 수 있습니다.

#### !default (초기값 설정)

`!default`플래그는 할당되지 않은 변수의 초깃값을 설정합니다.
즉, 할당되어있는 변수가 있다면 변수가 기존 할당 값을 사용합니다.

좀 더 유용하게, ‘변수와 값을 설정하겠지만, 혹시 기존 변수가 있을 경우는 현재 설정하는 변수의 값은 사용하지 않겠다’는 의미로 쓸 수 있습니다.

#### #{} (문자 보간)

`#{}`를 이용해서 코드의 어디든지 변수 값을 넣을 수 있습니다.

### 연산

**- 산술 연산자**
[색상연산자 실습](https://codesandbox.io/s/yjpklp489x)

| 종류 | 설명   | 주의사항                             |
| ---- | ------ | ------------------------------------ |
| -    | 더하기 |
| \*   | 빼기   |
| -    | 곱하기 | 하나 이상의 값이 반드시 숫자(Number) |
| /    | 나누기 | 오른쪽 값이 반드시 숫자(Number)      |
| %    | 나머지 |

**- 비교 연산자**

| 종류 | 설명                            |
| ---- | ------------------------------- |
| ==   | 동등                            |
| !=   | 부등                            |
| <    | 대소 / 보다 작은                |
| >    | 대소 / 보다 큰                  |
| <=   | 대소 및 동등 / 보다 작거나 같은 |
| >=   | 대소 및 동등 / 보다 크거나 같은 |

**- 논리(볼린, Boolean) 연산자**
|종류 |설명|
|and |그리고 (자바스크립트: `&&`)|
|or |또는 (자바스크립트: `||`)|
|not |부정 (자바스크립트: `!`)|

### 재활용 (Mixins)

Sass Mixins는 스타일 시트 전체에서 재사용 할 CSS 선언 그룹 을 정의하는 아주 훌륭한 기능입니다.

- 선언하기(`@mixin`)
- 포함하기(`@include`)

#### @mixin

`@mixin` 지시어를 이용하여 스타일을 정의합니다.

```scss
// SCSS
@mixin 믹스인이름 {
  스타일;
}

// Sass
=믹스인이름
  스타일
```

#### @include

선언된 Mixin을 사용(포함)하기 위해서는 `@include`가 필요합니다.

```scss
// SCSS
@include 믹스인이름;

// Sass
+믹스인이름
```

#### 인수

[mixin / include 실습](https://codesandbox.io/s/zw0lvlo924)

Mixin은 함수(Functions)처럼 인수(Arguments)를 가질 수 있습니다.
하나의 Mixin으로 다양한 결과를 만들 수 있습니다.

```scss
// SCSS
@mixin 믹스인이름($매개변수) {
  스타일;
}
@include 믹스인이름(인수);

// Sass
=믹스인이름($매개변수)
  스타일

+믹스인이름(인수)
```

**인수의 기본값 설정**

[ mixin / include 매개변수 기본값 ](https://codesandbox.io/s/239qvpmo8p)

인수(argument)는 기본값(default value)을 가질 수 있습니다.
`@include` 포함 단계에서 별도의 인수가 전달되지 않으면 기본값이 사용됩니다.

```scss
@mixin 믹스인이름($매개변수: 기본값) {
  스타일;
}
```

**키워드 인수**

[키워드 인수 실습](https://codesandbox.io/s/jlnyy6m4q5)

```scss
@mixin 믹스인이름($매개변수A: 기본값, $매개변수B: 기본값) {
  스타일;
}

@include 믹스인이름($매개변수B: 인수);
```

**가변 인수**

[가변 인수 실습](https://codesandbox.io/s/p77ow3j03j)
입력할 인수의 개수가 불확실한 경우가 있습니다.
그럴 경우 가변 인수를 사용할 수 있습니다.
가변 인수는 매개변수 뒤에 `...`을 붙여줍니다

```scss
@mixin 믹스인이름($매개변수...) {
  스타일;
}

@include 믹스인이름(인수A, 인수B, 인수C);
```

#### @content

[@content 실습](https://codesandbox.io/s/kk8lwwxp7v)

선언된 Mixin에 `@content`이 포함되어 있다면 해당 부분에 원하는 **스타일 블록** 을 전달할 수 있습니다.
이 방식을 사용하여 기존 Mixin이 가지고 있는 기능에 선택자나 속성 등을 추가할 수 있습니다.

```scss
@mixin 믹스인이름() {
  스타일;
  @content;
}

@include 믹스인이름() {
  // 스타일 블록
  스타일;
}
```

Mixin에게 전달된 스타일 블록은 Mixin의 범위가 아니라 스타일 블록이 정의된 범위에서 평가됩니다.
즉, Mixin의 매개변수는 전달된 스타일 블록 안에서 사용되지 않고 전역 값으로 해석됩니다.
전역 변수(Global variables)와 지역 변수(Local variables)에 대한 개념이 존재 한다.

### 확장(Extend)

[Extend 실습](https://codesandbox.io/s/pkqr96j05x)
특정 선택자가 다른 선택자의 모든 스타일을 가져야하는 경우가 종종 있습니다.
이럴 경우 선택자의 확장 기능을 사용할 수 있습니다.

```scss
@extend 선택자;
```

결과를 보면 ,로 구분하는 다중 선택자(Multiple Selector)가 만들어졌습니다.

사실 `@extend`는 다음과 같은 문제를 고려해야 합니다.

- 내 현재 선택자(위 예제의 .btn-danger)가 어디에 첨부될 것인가?
- 원치 않는 부작용이 초래될 수도 있는가?
- 이 한 번의 확장으로 얼마나 큰 CSS가 생성되는가?

결과적으로 확장(Extend) 기능은 무해하거나 혹은 유익할 수도 있지만 그만큼 부작용을 가지고 있을 수 있습니다.
따라서 확장은 사용을 권장하지 않으며, 위에서 살펴본 Mixin을 대체 기능으로 사용하세요.

사용을 권장하지 않는 이유에 대해서 좀 더 자세한 정보를 원하면 [Sass Guidelines Extend](https://sass-guidelin.es/ko/#extend)를 참고하세요.

### 함수(Function)

[함수 실습](https://codesandbox.io/s/94znlpn1zo)

**함수와 Mixins은 거의 유사하지만 반환되는 내용이 다릅니다.**

`Mixin`은 위에서 살펴본 대로 `지정한 스타일(Style)을 반환`하는 반면,
`함수`는 보통 연산된(Computed) 특정 값을 `@return 지시어를 통해 반환`합니다.

```scss
// Mixins
@mixin 믹스인이름($매개변수) {
  스타일;
}

// Functions
@function 함수이름($매개변수) {
  @return 값
}
```

사용하는 방법에도 차이가 있습니다.
Mixin은 `@include` 지시어를 사용하는 반면,
함수는 함수이름으로 바로 사용합니다.

```scss
// Mixin
@include 믹스인이름(인수);

// Functions
함수이름(인수)
```

**내장함수**

[내장 함수 실습](https://codesandbox.io/s/v39r8jrwp7)

위와 같이 함수는 `@include` 같은 별도의 지시어 없이 사용하기 때문에 내가 지정한 함수와 내장 함수(Built-in Functions)의 이름이 충돌할 수 있습니다.
따라서 내가 지정한 함수에는 별도의 접두어를 붙여주는 것이 좋습니다.

### 조건과 반복

#### if(함수)

[함수 실습](https://codesandbox.io/s/kw1qz744p3)

조건의 값(`true`, `false`)에 따라 두 개의 표현식 중 하나만 반환합니다.
[조건부 삼항 연산자(conditional ternary operator)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Operators/Conditional_Operator)와 비슷합니다.

조건의 값이 `true`이면 표현식1을,
조건의 값이 `false`이면 표현식2를 실행합니다.

```scss
if(조건, 표현식1, 표현식2)
```

#### @if (지시어)

[@if (지시어) 실습](https://codesandbox.io/s/krymy6q0o)

`@if` 지시어는 조건에 따른 분기 처리가 가능하며, if 문(if statements)과 유사합니다.
같이 사용할 수 있는 지시어는 `@else`, `if`가 있습니다.

```scss
// @if
@if (조건) {
  /* 조건이 참일 때 구문 */
}

// @if @else
@if (조건) {
  /* 조건이 참일 때 구문 */
} @else {
  /* 조건이 거짓일 때 구문 */
}

// @if @else if
@if (조건1) {
  /* 조건1이 참일 때 구문 */
} @else if (조건2) {
  /* 조건2가 참일 때 구문 */
} @else {
  /* 모두 거짓일 때 구문 */
}
```

조건에는 논리 연산자 `and`, `or`, `not`을 사용할 수 있습니다.
Sass의 내장 함수 `unitless()`는 숫자에 단위가 있는지 여부를 반환합니다.

[if 심화 실습](https://codesandbox.io/s/n9wzko3780)

#### @for

[for 실습](https://codesandbox.io/s/pyj9n7qnm7)

`@for`는 스타일을 반복적으로 출력합니다.
for 문과 유사합니다.

`@for`는 `through`를 사용하는 형식과 `to`를 사용하는 형식으로 나뉩니다.
두 형식은 종료 조건이 해석되는 방식이 다릅니다.

```scss
// through
// 종료 만큼 반복
@for $변수 from 시작 through 종료 {
  // 반복 내용
}

// to
// 종료 직전까지 반복
@for $변수 from 시작 to 종료 {
  // 반복 내용
}
```

변수는 관례상 `$i`를 사용합니다.

`to`는 주어진 값 직전까지만 반복해야할 경우 유용할 수 있습니다.
그러나 **`:nth-child()`에서 특히 유용하게 사용되는 `@for`는 일반적으로 `through`를 사용하길 권장합니다.**

#### @each

`@each`는 List와 Map 데이터를 반복할 때 사용합니다.
`for in` 문과 유사합니다.

```scss
@each $변수 in 데이터 {
  // 반복 내용
}
```

**동시에 여러 개의 List 데이터를 반복 처리**
[each List 실습](https://codesandbox.io/s/zqmyy5lq2p)

**Map 데이터를 반복할 경우**
[each map 실습](https://codesandbox.io/s/j1vrxvq159)

```scss
@each $key변수, $value변수 in 데이터 {
  // 반복 내용
}
```

#### @while

`@while`은 조건이 `false`로 평가될 때까지 내용을 반복합니다.
while 문과 유사하게 잘못된 조건으로 인해 컴파일 중 무한 루프에 빠질 수 있습니다.
**사용을 권장하지 않습니다.**

```scss
@while 조건 {
  // 반복 내용
}
```

### 내장함수

Sass에서 기본적으로 제공하는 내장 함수에는 많은 종류가 있습니다.

[Sass Built-in Functions](http://sass-lang.com/documentation/Sass/Script/Functions.html)에서 모든 내장 함수를 확인할 수 있습니다.

- []는 선택 가능한 인수(argument)입니다.
- Zero-based numbering을 사용하지 않습니다.

#### 색상(RGB / HSL / Opacity) 함수

`mix($color1, $color2)` : 두 개의 색을 섞습니다.

`lighten($color, $amount)` : 더 밝은색을 만듭니다.

`darken($color, $amount)` : 더 어두운색을 만듭니다.

`saturate($color, $amount)` : 색상의 채도를 올립니다.

`desaturate($color, $amount)` : 색상의 채도를 낮춥니다.

`grayscale($color)` : 색상을 회색으로 변환합니다.

`invert($color)` : 색상을 반전시킵니다.

`rgba($color, $alpha)` : 색상의 투명도를 변경합니다.

`opacify($color, $amount) / fade-in($color, $amount)` : 색상을 더 불투명하게 만듭니다.

`transparentize($color, $amount) / fade-out($color, $amount)` : 색상을 더 투명하게 만듭니다.

#### 문자(String) 함수

`unquote($string)` : 문자에서 따옴표를 제거합니다.

`quote($string)` : 문자에 따옴표를 추가합니다.

`str-insert($string, $insert, $index)` : 문자의 index번째에 특정 문자를 삽입합니다.

`str-index($string, $substring)` : 문자에서 특정 문자의 첫 index를 반환합니다.

`str-slice($string, $start-at, [$end-at])` : 문자에서 특정 문자(몇 번째 글자부터 몇 번째 글자까지)를 추출합니다.

`to-upper-case($string)` : 문자를 대문자를 변환합니다.

`to-lower-case($string)` : 문자를 소문자로 변환합니다.

#### 숫자(Number) 함수

`percentage($number)` : 숫자(단위 무시)를 백분율로 변환합니다.

`round($number)` : 정수로 반올림합니다.

`ceil($number)` : 정수로 올림합니다.

`floor($number)` : 정수로 내림(버림)합니다.

`abs($number)` : 숫자의 절대 값을 반환합니다.

`min($numbers…)` : 숫자 중 최소 값을 찾습니다.

`max($numbers…)` : 숫자 중 최대 값을 찾습니다.

`random()` : 0 부터 1 사이의 난수를 반환합니다.

#### List 함수

모든 List 내장 함수는 기존 List 데이터를 갱신하지 않고 새 List 데이터를 반환합니다.
모든 List 내장 함수는 Map 데이터에서도 사용할 수 있습니다.

`length($list)` : List의 개수를 반환합니다.

`nth($list, $n)` : List에서 n번째 값을 반환합니다.

`set-nth($list, $n, $value)` : List에서 n번째 값을 다른 값으로 변경합니다.

`join($list1, $list2, [$separator])` : 두 개의 List를 하나로 결합합니다.

`zip($lists…)` : 여러 List들을 하나의 다차원 List로 결합합니다.

`index($list, $value)` : List에서 특정 값의 index를 반환합니다.

#### Map 함수

모든 Map 내장 함수는 기존 Map 데이터를 갱신하지 않고 새 Map 데이터를 반환합니다.

`map-get($map, $key)` : Map에서 특정 key의 value를 반환합니다.

`map-merge($map1, $map2)` : 두 개의 Map을 병합하여 새로운 Map를 만듭니다.

`map-keys($map)` : Map에서 모든 key를 List로 반환합니다.

`map-values($map)` : Map에서 모든 value를 List로 반환합니다.

#### 관리(Introspection) 함수

`variable-exists(name)` : 변수가 현재 범위에 존재하는지 여부를 반환합니다.(인수는 \$없이 변수의 이름만 사용합니다.)

`unit($number)` : 숫자의 단위를 반환합니다.

`unitless($number)` : 숫자에 단위가 있는지 여부를 반환합니다.

`comparable($number1, $number2)` : 두 개의 숫자가 연산 가능한지 여부를 반환합니다.

## 설계

UI, 페이지 등 .... 폴더별로 설계를 합니다. 그런데 아마도 작업자에 따라 회사 별로 폴더 설게가 다르겠죠??

그사람은 이렇게 설계 하는 이유는 유지보수를 좋게 하기위해서 래요. 저는 실무에서 이방법을 사용했어요. 개인적으로 유지보수에는 괜찮았어요. 참고로 강사님이 알려주신 `module.css`가 협업에서 더 많이 사용할 수 있어요!(사실 잘 뭐가 더 많이 사용하는지 잘 몰라요.... 추측...)

```js
import styles from "./Button.module.css"; // Import css modules
```

[sass-guidelin 설계 방법론](https://sass-guidelin.es/ko/#sass-)

### 컴퍼넌트

대부분의 `인터페이스`는 `작은 컴퍼넌트`들로 생각될 수 있으며 이러한 인식을 고수할 것을 강력히 추천합니다. 예를 들면, `검색 폼`은 `컴퍼넌트로 취급`되어야 합니다. 그것은 다른 위치, 다른 페이지에서, 다양한 상황에서 `재사용이 가능`해야 합니다.

### 패턴(폴더 분리?)

CSS 스타일시트로 컴파일하는 루트 레벨에 있는 하나의 파일(대개 main.scss)을 갖게 됩니다.

- base/
  - HTML 요소에 대한 표준 스타일을 정의하는 스타일시트
- components/
  - layout/이 (전반적인 뼈대를 정의하는) 거시적인 폴더임에 반해, components/는 위젯에 초점을 둡니다. 이 폴더는 슬라이더, 로더, 위젯, 그리고 기본적으로 이들과 비슷한 것을 비롯해 온갖 구체적인 모듈들을 담습니다.
- layout/
  - 사이트의 주요 부분(header, footer, navigation, sidebar…), 그리드 시스템 혹은 모든 폼의 스타일을 위한 스타일시트
- pages/
  - 페이지에 한정된 스타일이 있는경우 페이지 이름을 딴 파일을 넣습니다.
- themes/
  - 다른 여러 테마를 여기에 전부 모아둡니다.
- utils/
  - sass 도규와 헬퍼를 모읍니다. 모든 전역 변수, 함수, 믹스인, 플레이스홀더가 들어갑니다.
- vendors/
  - 외부 라이브러리와 프레임워크에서 나오는 모든 CSS 파일을 담고 있는 vendors/ 폴더를 가집니다.

```
sass/
|
|– base/
|   |– _reset.scss       # Reset/normalize
|   |– _typography.scss  # 타이포그래피 규칙
|   …                    # 기타.
|
|– components/
|   |– _buttons.scss     # 버튼
|   |– _carousel.scss    # 캐러셀
|   |– _cover.scss       # 커버
|   |– _dropdown.scss    # 드롭다운
|   …                    # 기타.
|
|– layout/
|   |– _navigation.scss  # 네비게이션
|   |– _grid.scss        # 그리드 시스템
|   |– _header.scss      # 헤더
|   |– _footer.scss      # 푸터
|   |– _sidebar.scss     # 사이드바
|   |– _forms.scss       # 폼
|   …                    # 기타.
|
|– pages/
|   |– _home.scss        # 홈 한정 스타일
|   |– _contact.scss     # 연락처 한정 스타일
|   …                    # 기타.
|
|– themes/
|   |– _theme.scss       # 디폴트 테마
|   |– _admin.scss       # 관리자 테마
|   …                    # 기타.
|
|– utils/
|   |– _variables.scss   # Sass 변수
|   |– _functions.scss   # Sass 함수
|   |– _mixins.scss      # Sass 믹스인
|   |– _helpers.scss     # 클래스 & 플레이스홀더 헬퍼
|
|– vendors/
|   |– _bootstrap.scss   # Bootstrap
|   |– _jquery-ui.scss   # jQuery UI
|   …                    # 기타.
|
|
`– main.scss             # 메인 Sass 파일
```

폴더안에 존재하는 파일 이름 앞에 `_`(언더 스코어)를 붙여(\_header.scss와 같이) @import로 가져오면 컴파일 시 ~.css 파일로 컴파일하지 않습니다.

### Main 파일 (상위 Sass파일)

(주로 main.scss로 이름이 붙는) 메인 파일은 전체 코드베이스에서 언더스코어로 시작하지 않는 유일한 Sass 파일이어야 합니다. 이 파일은 @import와 주석 외에는 아무 것도 포함하지 않아야 합니다.

파일들은 각자 자리 잡은 폴더에 따라 순서대로 하나하나 불러들여집니다.
가독성을 유지하기 위해, 메인 파일은 이 가이드라인을 준수해야 합니다:

1. `@import 당 파일 하나`
1. `한 줄에 하나`의 @import
1. 같은 폴더로부터의 두 import 사이는 `새 줄로 띄우지 않는다`
1. 한 폴더로부터의 `마지막 import` 다음에는 `새 줄 하나로 간격`을 둔다.
1. 파일 확장자와 앞에 붙는 `언더스코어는 생략`한다.

## [실습] 해보아요 ~~~~~!!!!

- FDS-REACT-TODOLIST로 실습을 하겠습니다.
- [저꺼 FDS-REACT-TODOLIST인데요~](https://github.com/kimseulbi/fds-react-todolist) 여기서 TODOLiST html 마크업을 참고하셔도 되고 아님 기존에 있는 그대로를 사용하셔도 되요. 나는 없다 하면 clone 해서 api.js에서 axios내 서버 주소 등록 해주세요.

## 다 같이 부트스트랩 sass를 보아요!

[부트스트랩](http://bootstrapk.com/getting-started/)

# 참고한 링크 및 출처

[Sass documentation](https://sass-lang.com/documentation/file.SASS_REFERENCE.html)

[sass-guidelin](https://sass-guidelin.es/ko/#sass-)

[https://heropy.blog/2018/01/31/sass/](https://heropy.blog/2018/01/31/sass/)

[bbol-world.tistory](https://bbol-world.tistory.com/80)
