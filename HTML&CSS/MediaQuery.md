# 반응형 웹 vs 적응형 웹

반응형 웹은 하나의 템플릿을 사용해 모든 기기에 대응하는데 반해, 적응형 웹은 선별된 기기 유형에 따라 별도의 독립적인 템플릿이 요구됩니다. 즉, 별도 페이지 제작이 필요합니다. 적응형 웹이 반영된 예로 NAVER, DAUM 같은 포털 사이트를 들 수 있는데 기존부터 서비스 되고 있는 사이트 변경 없이, 모바일 환경에 대응하기 위해 별도의 URL을 통해 서비스 합니다. 모바일 환경에서 기존 사이트 주소로 접속할 경우, 보통은 이를 감지하여 모바일 전용 페이지로 리디렉션(redirection) 합니다.

![](http://yamoo9.github.io/cj-olive-networks/assets/rwd/awd-rwd.jpg)

# Viewport meta tag

색엔진최적화(SEO)를 위해 검색엔진에게 메타데이터를 전달하기 위해 사용되는데, viewport meta tag는 브라우저의 화면 설정과 관련된 정보를 제공합니다.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
```

**뷰포트 메타 태그 있을 때**

```html
<meta name="viewport" content="width=device-width, initial-scale=1" />
```

# @Media : 미디어쿼리

`@media`을 사용하여 미디어 별로 style을 지정하는 것을 미디어쿼리라고 합니다. 디바이스를 지정하는 것뿐만 아니라 디바이스의 크기나 비율까지 구분할 수 있습니다.
Media Query의 문법은 아래와 같습니다.

```css
@media not|only mediatype and (expressions) {
  CSS-Code;
}
```

### `and` 혹은 `,`

`and` 연산자는 복잡한 미디어 특성들이 서로 연결되거나 미디어 특성과 미디어타입을 연결시키는데 사용됩니다. 기본적으로 미디어쿼리(미디어 타입이 all 로 지정된 미디어특성)은 다음과 같이 표시하는것이 가능합니다.

```css
@media (min-width: 700px) and (orientation: landscape) {
  /* 디스플레이가 700px 이상 크기이며 가로방향으로 되어있을 경우 */
}
```
