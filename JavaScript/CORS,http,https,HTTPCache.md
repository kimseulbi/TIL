# CORS (Cross-Origin Resource Sharing)

[크로스도메인요청CORS](https://brunch.co.kr/@adrenalinee31/1)

<!-- 에이잭트대해서 배울때 단점으로  외부 서버의 경로 ajax요청을 날리면 에러가 나면서 요청 실패한다.라고 배웠잔아요. 왜 실패를 하는지 알아보겠습니다. 브라우저에서 아래와 같이 에러가 나는데요. 외부로 요청이 안되는것은 자바스크립트 엔진 표준 스펙에 동일 출처 정책이라는 보안규칙이 있기 때문입니다. -->

<!-- 동일 출처 정책은 애플리케이션 보안모델에 중요한 개념중 하나입니다.
이 정책에 의해서 자바스크립트로 다른 웹페이지에 접근할 때 같은 출처의 페이지만 접근이 가능합니다. 같은 출처라는 것은 `프로토콜`, `호스트명`, `포트`가 같다는 것을 의미합니다.
즉, 웹페이지의 스크립트는 그 페이지와 같은 서버에 있는 주소만 ajax 요청을 할 수 있다는 것입니다.

CORS에 대해서 설명하기 전에 서버의 도움 없이 동일 출처 정책을 회피하여 외부 서버로 요청을 날릴수 있는 방법 소개

우리 프로젝트 할때 이문제로 백엔드개발자에서 요청하라고 선생님이 알려주신적이 있어요
 -->

> 외부 서버의 경로 ajax요청을 날리면 에러가 나면서 요청 실패한다. 이는 자바스크립트 엔진 표준 스펙에 동일 출처 정책이라는 보안규칙이 있기 때문입니다.

## Same-origin Policy(동일 출처 정책)

- 웹페이지에서 리소스를 불러올 때, 리소스의 출처가 웹페이지의 출처와 같으면 안전하다고 보고, 출처가 다르면 해당 리소스는 안전하지 않다고 보는 원칙
- 여기서 '출처'란 '프로토콜 + 도메인 + 포트번호'의 결합을 가리킴. 즉, 세 개가 다 같아야 동일 출처라고 할 수 있고, 셋 중에 하나라도 다르면 동일 출처로 간주되지 않음
- 웹 보안의 기본 원칙으로, 웹 브라우저의 많은 요소에 적용됨

![동일출처정책](./asset/동일출처정책.png)

요즘 여러 도메인에 걸쳐서 구성되는 대규모 웹 프로젝트가 늘어나고, REST API 등을 이용한 외부 호출이 많아지는 상황에서는 거추장스러운 기술이 되기도하고 있다. 그래서 만들어진 추가 정책이 CORS이다.

<!-- 렙러전테이셔널 스테이트 트랜스퍼 -->

> 🔖 REST API(Representational state transfer)\
> 월드와이드웹과 같은 분산 하이퍼미디어 시스템에서 운영되는 소프트웨어 아키텍처스타일입니다.
> https://meetup.toast.com/posts/92

## CORS란? (Cross-Origin Resource Sharing)

- **클라이언트 측 cross-origin 요청**을 **안전하게 보낼 수 있는 방법**을 정한 표준
- **스크립트가 전혀 다른 출처를 갖는 API 서버를 사용하려고 하는 상황**에서는 뭔가 **추가적인 처리**를 해주어야한다는것.

# HTTP/ HTTPS

Web browser와 Web server 통신을 규칙인 HTTP/HTTPS

> **웹구성 4가지**\
> 페이지를 만드는 언어 `HTML`\
> 원하는 웹피이지에 방문할수 있도록 도와주는 주소 체계 `URL`, `URI`\
> 웹페이지를 주고 받는 소프트웨어인 `웹브라우저`, `웹서버`\
> Web browser와 Web server 통신을 규칙인 `HTTP`,`HTTPS`

## HTTP(HyperText Transfer Protocol)란?

![http](./asset/http.png)

```
고객이 클라이언트👨🏻‍💼, 캐셔가 서버👩🏻‍🌾, 물건이 http🥕
클라이언트가 요청(Request)하면 서버가 응답(Response) 합니다.
http는 Request와 Response를 나나냅니다.  HTML, CSS, JS, 이미지 등... 콘텐츠들을 클라이언트와 서버가 주고 받기 위해서 서로 알아 듣기위해서 공통의 약속이 메시지가 html입니다.
```

![HTTP 프로토콜](https://ssl.pstatic.net/sstatic/search/webmaster/2017/img/img_guide_13.jpg)

1. Browser (IE, Chrome, Safari, Firefox)가 web server와 통신하기 위한 규약
2. Browser에서 요청(Request)하면 응답(Response)하는 간단한 구조(프로토콜)

**`HTTP`로 통신을 한다면 암호화가 되어있지 않기 때문에 서보와 클라이언트가 서로 주고받응 메시지를 알아개내기가 쉽습니다.(보안 취약)**

## HTTPS(Hyper Text Transfer Protocol Secure)란?

![HTTPS](https://i.imgur.com/tq9mmGg.png)

브라우저와 연결된 웹 사이트간에 데이터를 전송하는 프로토콜 인 HTTP의 보안 버전입니다.

**HTTPS 끝의 "S"**는 **보안**을 나타냅니다. 그것은 귀하의 브라우저와 웹 사이틀 간의 모든 통신이 암호화되었음을 의미합니다.

웹브라우저는 주소 표시 줄에 자물쇠 아이콘을 표시하여 HTTPS 연결이 유효함을 시각적으로 나타냅니다.

HTTPS와 SSL를 같은 의미로 이해하지만. 이것은 맞기도 틀리기도 하다. 그것은 마치 인터넷과 웹을 같은 의미로 이해하는 것과 같다. 결론적으로 말하면 웹이 인터넷 위에서 돌아가는 서비스 중의 하나인 것처럼 HTTPS도 SSL 프로토콜 위에서 돌아가는 프로토콜이다.

### HTTPS는 어떻게 작동할까요?

![http&https](https://www.instantssl.com/images/http-vs-https.png)

## SSL 디지털 인증서

- 클라이언트와 서버간의 통신을 공인된 제3자업체(CA)가 보증해주는 전자화된 문서

> 🔖 CA (Certificate Authority)\
> 디지털 인증를 제공하는 공인 기업

### SSL 인증서의 장점 및 역할

- 통신 내용이 노출, 변경되는 것을 방지
- 클라이언트가 접속하려는 서버가 신뢰 할 수 있는 서버인지 확인가능
- SSL통신에 사용할 공개키를 클라이언트에게 제공

### SSL 암호화 종류

**1. 대칭키**
암호를 만드는 행위인 암호화를 할 때 사용하는 일종의 비밀번호을 키라고 한다.

> 🔖 인코딩, 디코딩\
> 인코딩이랑 정보를 부호화/암호화, 디코딩은 부호화/암호화를 해제

**2.. 공개키**

### SSL 동작방법

- 공개키 암호 방식은 알고리즘 계산방식이 느린 경향이 있다.
- 따라서 SSL은 암호화된 데이터를 전송하기 위해서 공개키와 대칭키 암호화 방식을 혼합하여 사용한다.
- 안전한 의사소통 채널을 수립할 때는 공개키 암호를 사용하고, 이렇게 만들어진 안전한 채널을 통해서 임시의 무작위 대칭키를 생성 및 교환한다. 해당 대칭키는 나머지 데이터 암호화에 활용한다.
  - 실제 데이터 암호화 방식 : 대칭키
  - 상기 대칭키를 서로 공유하기 위한 암호화 방식 : 공개키

### SSL 통신방법

![SSL 통신방법](https://i.imgur.com/YIfy1wK.png)

[생활코딩 HTTPS와 SSL 인증서 심화(서버) 알고 싶다면](https://opentutorials.org/course/228/4894)

## HTTPS 장점

**1. HTTPS는 HTTP보다 빠르다** ︎︎✔︎

![](http://optimal.inven.co.kr/upload/2018/08/26/bbs/i16228280124.gif)

[HTTPS는 HTTP보다 빠르다](https://tech.ssut.me/https-is-faster-than-http/)

[확인해볼까요???? 누가 빠르나?](http://www.httpvshttps.com/)

**2. 구글 노출 랭킹에 도움이 된다.** ✔︎  
![](https://gobooki.net/wp-content/uploads/2018/07/https%EA%B0%80-%EA%B5%AC%EA%B8%80-%EB%9E%AD%ED%82%B9-%EC%8B%9C%EC%8A%A4%ED%85%9C%EC%97%90-%EC%98%81%ED%96%A5.png)

**3. ATS(IOS App Transport Secutiry)는 HTTP를 차단**
![](https://gobooki.net/wp-content/uploads/2018/07/ios-https.png)

**4. PWA(Progressive Web Apps)에는 https만 가능**
![](https://gobooki.net/wp-content/uploads/2018/07/progressive-web-app.png)

**5. 지리정보, 자동기입 등의 모든 API는 https가 필요함**
![](https://gobooki.net/wp-content/uploads/2018/07/https-modern-apis.png)

**6. https는 도입비용이 비싸지 않음**

**7. 안전하다.**

# HTTP Cache

## Cache 만들어진 배경

웹이 만들어진 이후에 많은 삶이 달라지면서 사람은 욕심은 증가했습니다. 데이터가 급증하여 데이터의 속도를 증가 시키기위해서 생겨났습니다.

## Cache란?

돈이 아니라 저장한다는 의미입니다.

한번 다운로드받은 파일을 다시 받지 않고 컴퓨터에 저장 즉 캐시 했다가 같은 주소로 접속한다면 캐시해둔 파일을 사용한다면 네트워크 지연으로 인한 속도저하를 막을수 있는 방법입니다.

- 자원의 효율적 로딩을 위한 웹 표준
- 서버에서 가져온 자원(HTML, CSS, JS, 이미지, ...)을 가까운 곳(브라우저, 혹은 다른 서버)에 저장해놓고 재사용
- 캐시를 할 것인지 말 것인지, 어떻게 할 것인지를 결정하는 규칙이 복잡하고, 브라우저마다 조금씩 다름

> **Cache의 안타까움**\
> 캐시를 최신상태를 유지하는 방법이 어렵습니다....
> 내용이 갱신되었을때도 그사실을 웹브라우저라면 알지 못합니다.

## 캐시 제어 방법

```
* 웹브라우저 캐시 비우기(갱신)*
Windows: Ctrl + F5
MacOS: Cmd + R
Linux: F5
```

일반 사용자를 위해 만들어진것들을 소개 하겠습니다.

### 1. cache-control

TODO

### 2. pragma

TODO

### 캐시적용

TODO

[생활코딩 httpCache 강의](https://opentutorials.org/module/3830/22985)

# 🎉 (추가) 개발자가 꼭 알아야 할 보안

- 다 같이 읽어보아요!!! -> [개발자가 꼭 알아야 할 보안이야기](https://www.slideshare.net/deview/d2-campus-seminar-45210063?fbclid=IwAR0hFi9I4-WqdI8RntdBl1StI0hcgMWv85dAHbHkmmrSPW1YfDLfCQkznN0)

- 활용해 보아요.📝\
  [개발자가 알아할 보안리스트](https://github.com/FallibleInc/security-guide-for-developers/blob/master/security-checklist.md)

# 면접 문제

1. CORS에 대해 설명할 수 있나?
1. http 프로토콜에서 https이미지를 불러올 수 있나? 불러온다면 어떠한 문제가 있을까. warning을 없앨 수 있는 방법은 무엇일까?
