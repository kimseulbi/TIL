# SPA (Single Page Application)

단일 페이지 애플리케이션는 모던 웹의 패러다임이다. SPA는 **기본적으로 단일 페이지**로 구성되며기존의 서버 사이드 렌더링과 비교할 때, **배포가 간단**하며 네이티브 앱과 유사한 사용자 경험을 제공하는 장점이 있습니다.

link tag를 사용하는 전통적인 웹 방식(서버 사이드 랜더링)은 새로운 페이지 요청 시마다 정적 리소스가 다운로드되고 전체 페이지를 다시 렌더링하는 방식을 사용하므로 새로고침이 발생되어 사용성이 좋지 않다. 그리고 변경이 필요없는 부분을 포함하여 전체 페이지를 갱신하므로 비효적입니다.

SPA는 기본적으로 웹 애플리케이션에 필요한 **모든 정적 리소스를 최초에 한번 다운로드** 한다. 이후 새로운 페이지 요청시, 페이지 갱신에 필요한 데이터만을 전달받아 페이지를 갱신하므로 전체적인 트래픽을 감소할 수 있고, 전체 페이지를 다시 렌더링 하지 않고 변경되는 부분만을 갱신하므로 새로고침이 발생하지 않아 네이티브 앱과 유사한 사용자 경험을 제공할 수 있다.

모바일의 사용이 증가하고 있는 현 시점에 트래픽의 감소와 속도, 사용성, 반응성의 향상은 매우 중요한 이슈이다. SPA의 핵심 가치는 **사용자 경험(UX) 향상**에 있으며 부가적으로 **애플리케이션 속도의 향상**도 기대할 수 있어서 모바일 퍼스트(Mobile First) 전략에 부합한다.

# 서버 사이드 렌더링 & 클라이언트 사이드 렌더링

![](https://cdn-images-1.medium.com/max/1600/0*SnBCpaOXrQFYdFU6.)

저번시간에 모듈번들러와 모듈로더 개념이랑 비슷한거 같아요!!!

[클라이언트 렌더링에 대한 서버사이드 렌더링의 이점](https://medium.com/walmartlabs/the-benefits-of-server-side-rendering-over-client-side-rendering-5d07ff2cefe8)

<!-- walmart.com 이기는 서버사이드렌더링을 사용하고 있데요. 이유는 고객을 위한 성늘 혜택이랑 일관된 SEO 성능 때문이라고 해요.그런데 성능을 최적화하기에 시간과 노력이 많이 필요했데요. -->

## 서버 사이드 렌더링 이란? (SSR)

`전통적인 웹 페이지 방식 = SSR`

**서버에서 렌더링이 일어나는 경우**를 말합니다.
기존에 존재하던 방식으로 사용자가 웹페이지에 접근할 때, 서버에 페이지에 대한 요청을 하며 서버에서는 html, view와 같은 리소스들을 어떻게 보여질지 해석하고 렌더링하여 사용자에게 반환합니다. 이는 요청시마다 새로고침이 일어나면 서버에 새로운 페이지에 대한 요청을 하는 방식입니다.

간단하게 설명하면 먹고 싶은것이 **있을 때마다 슈퍼마켓에 가는것**과 비슷합니다.

![SSR 방식](https://jongmin92.github.io/images/post/2017-06-06/server_side_rendering_1.png)
![](https://cdn-images-1.medium.com/max/1600/1*jJkEQpgZ8waQ5P-W5lhxuQ.png)

```
SSR의 경우 브라우저에 대한 서버의 응답은 렌더링 준비가 된 페이지의 HTML이고 사용자는 모든 상황이 진행되는 동안 페이지를 볼 수 있습니다.
[참고] SSR에서는 빈페이지가 깜빡이고 SSR에서는 실제로 발생하지 않습니다.
대부분의 사람들은 모든 이미지가 로드 될 때 제거되는 서버 응답에서 로드되는 이미지를 보내야 피할 수 있습니다.
```

### SSR 특징

- 페이지가 더 일찍 렌더링되고 고객이 페이지를 더 빨리 볼 수는 있지만 반응이 실행되기 전에는 실제로 페이지와 상호 작용할 수 없습니다. 고객이 정말로 빠르게 버튼을 클릭 하면 작업이 실행이 되지 않습니다.

- SSR **첫로딩**은 매우 짧지만 페이지 마다 서버에 로딩을 해야되기 때문에 전체적으로는 에 CSR보다 느립니다 .

- 서버의 SSR 처리량은 CSR 처리량보다 훨씬 적습니다. 특히 반응에 대한 처리량 영향은 매우 큽니다. `ReactDOMServer.renderToString`은 이벤트 루프를 보유하는 동기 CPU 바운드 호출입니다. 즉, 서버는 `ReactDOMServer.renderToString`완료 될 때까지 다른 요청을 처리 할 수 ​​없습니다 . 페이지를 SSR 처리하는 데 500ms가 걸리므로 최대 초당 2 회의 요청을 처리 할 수 ​​있습니다.

## 클라이언트 사이드 렌더링 이란? (CSR)

최초에 1번 서버에서 전체 페이지를 로딩하여 보여주고 이후에는 사용자의 요청이 올 때마다, 리소스를 서버에서 제공한 후 클라이언트가 해석하고 렌더링을 하는 방식입니다. 즉,`서버`는 단지 `JSON 파일만 보내주는 역할`을 하며 `html을 그리는 역할`은 `클라이언트 측에서 자바스크립트가 수행합니다.` 여기서 Angular JS, Backbone JS같이 SPA 개발에 쉬운 JS 프레임워크가 등장했습니다. 하지만 점점 클라이언트가 무거워지자 다시 view만 관리하자는 철학으로 React JS가 등장하게 되었습니다. 곧 SPA가 CSR 방식을 사용한 것입니다.

`(주의점)`기존 웹에서 사용하는 방식이 모두 SSR이 아닌 것 처럼 SPA 방식이 모두 CSR가 아닙니다.

CSR은 슈퍼마켓에 한 번 방문하고 좀 더 시간을 들여 꽤 오랜 기간동안 먹을 음식을 구매합니다. 그런 다음, 먹고 싶은 것이 있을 때마다 슈퍼마켓에 가지 않고 냉장고에서 찾게됩니다.

![CSR 방식](https://jongmin92.github.io/images/post/2017-06-06/client_side_rendering_1.png)

> 🔖 런타임\
> 프로그램밍 언어가 구동되고 있는 환경

![](https://cdn-images-1.medium.com/max/1600/1*CRiH0hUGoS3aoZaIY4H2yg.png)

```
CSR의 경우 브라우저가 자바스크립트에 대한 링크가 있는 빈 문서를 얻는 것입니다. CSR은 모든일이 일어날 때까지 기다린 다음 가상 DOM을 페이지를 볼 수 있도록 브라우저 돔으로 이동시킵니다.
```

### CRS 특징

- CSR의 경우 서버에서 View를 렌더하지 않고 HTML 다운 + JS파일 + 각종 리소스 다운을 받은 후 브라우져에서 렌더링을 하기 때문에 **SSR보다는 초기 View 로딩 속도는 오래걸린다.**

- CSR의 경우 사용자의 행동에 따라 필요한 부분만 다시 읽어들이기 때문에 서버 측에서 렌더링하여 전체 페이지를 다시 읽어들이는 것보다 빠른 인터랙션이 가능하다.

- CSR은 페이지를 읽어들이는 시간 + JS를 읽어들이는 시간 + 그리고 JS가 화면을 그리는 시간 위 작업이 완료 후 콘텐츠가 사용자에게 보여지므로 웹 서버에서 콘텐츠 데이터라도 가져와야 한다면 그 시간은 더욱 길어진다.

## SSR와 CSR의 차이점

이둘의 차이점은 크게 렌더링 방식,렌더링 속도, SEO, 보안으로 볼 수 있습니다.

**1.. 렌더링 방식 및 속도**
![](https://cdn-images-1.medium.com/max/2000/0*-EWG5MXBIo-D_ug3.)

위에서 소개 했드시 SSR과 CSR는 렌더링 방식이 달랐습니다. SSR 렌더링이 빨라지고 CSR을 사용하면서 로드하는 동안 빈페이지가 나타납니다. CSR을 사용하는 대부분의 응용 프로그램은 빈 흰색 페이지를 로딜 아이콘으로 대체합니다.
![](https://cdn-images-1.medium.com/max/1600/1*7LcOn9FuMR6uE0PT2htrJg.png)

위에 이미지는 카테고리 및 검색 페이지에 대한 첫 번째 서버 응답입니다. 녹색막대는 네트워크 그래프의 나머지 부분과 비교해 상대적입니다. 여기서 참고해야되는 것은 문서크기와 시간입니다. 서버가 페이지에 HTML로 응답하기 떄문에 SSR의 문서 크기각 항상 더 크다는 것을 알 수 있습니다. 그리고 CSR응답이 더 빠릅니다.

> 🔖 렌더링\
> 어떤 웹페이지 접속시 그 페이지를 화면에 그려주는 것

**2. SEO 문제**

- **SEO(검색 엔진 최적화)**의 문제가 존재한다.
- CSR방식으로 이루어진 사이트에서는 View를 생성하기위해 자바스크립트를 실행시켜야 하며 대부분의 웹 크롤러 봇들은 자바스크립트 파일을 실행시키지 못한다. 때문에 HTML에서만 콘텐츠를 수집하게 되고 CSR 페이지를 빈페이지로 인식하게 된다.
- SSR은 View를 서버에서 전부 렌더링하여 내려주므로 HTML에 모든 컨텐츠가 저장되어 있기 때문에 SEO 적용에 큰 문제가 없습니다.

```
SPA는 서버 렌더링 방식이 아닌 자바스크립트 기반 비동기 모델(클라이언트 렌더링 방식)이다. 따라서 SEO는 언제나 단점으로 부각되어 왔던 이슈이다.
하지만 SPA는 정보의 제공을 위한 웹페이지보다는 애플리케이션에 적합한 기술이므로 SEO 이슈는 심각한 문제로 볼 수 없다.
Angular 또는 React 등의 SPA 프레임워크는 서버 렌더링을 지원하는 SEO 대응 기술이 이미 존재하고 있어 SEO 대응이 필요한 페이지에 대해서는 선별적 SEO 대응이 가능하다.
```

<!-- ```html
<iframe
  width="560"
  height="315"
  src="https://www.youtube.com/embed/BNHR6IQJGZs"
  frameborder="0"
  allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture"
  allowfullscreen
></iframe>
``` -->

[![](https://img.youtube.com/vi/BNHR6IQJGZs/0.jpg)](https://www.youtube.com/embed/BNHR6IQJGZs)

**3. 보안 문제**

- **SSR**에서는 사용자에 대한 정보를 **서버 측**에서 **세션**으로 관리를 했다.
- 그러나 **CSR**일 경우 **쿠키**말고는 사용자에 대한 정보를 저장할 공간이 마땅치 않다.

# 참고한 링크

[SSR/CSR](http://brownbears.tistory.com/411)
[medium The Benefits of Server Side Rendering Over Client Side Rendering](https://medium.com/walmartlabs/the-benefits-of-server-side-rendering-over-client-side-rendering-5d07ff2cefe8)
[poiemaweb Single Page Application](https://poiemaweb.com/js-spa)
[[번역] Client-side rendering VS. Server-sde rendering](https://jongmin92.github.io/2017/06/06/JavaScript/client-side-rendering-vs-server-side-rendering/?fbclid=IwAR1thlPyzfCnIngeDTr25vAZQjxlJpILX3tMk0JiVH89zHEZqBusrxAiz3c#2)

# 면접 문제

1. SPA(Single Page Application)로 구성된 페이지에서 SEO(Search Engine Optimization)를 할 수 있는 방법은 무엇일까?

1. SSR(Server Side Rendering)은 무엇이고 사용 목적은 무엇인가?
