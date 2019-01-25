# GraphQL&Testing

## 브라우저

### 웹브라우저란?

- HTML 문서와 그림, 멀티미디어 파일등 월드 와이드 웹(www)을 기반으로 한 인터넷의 컨텐츠를 검색 및 열람하기 위한 응용 프로그램의 총칭.

- 크롬, 오페라, 파이어폭스, 사파리 등등.

### 브라우저 구조

![브라우저 구조](https://d2.naver.com/content/images/2015/06/helloworld-59361-1.png)

### 웹의 동작 원리

**부제: 브라우저 주소창에 `www.google.com` 을 쳤을 때 일어나는 일**
![](https://xvp.akamaized.net/assets/customer_tools/dns_leak/dns-explained@2x-7de1937bc533d8f5c3a401cb76c799ec.png)

1. DNS 서버 (Domain Name Server)

- www.google.com이라는 **호스트 네임**에 매치되는 ip 주소를 얻는다.
- **DNS 서버 : 호스트 네임을 ip 주소를 매칭시켜주는 서버**

packit단위로 파일을 쪼개서 보내줍니다.

프로토콜 - 언어의 규칙 대화방식이라고 생각하라

## Rest란? Rest api란?! Restful이란?!?!?

- **REpresentational State Transfer 의 약자**
- `HTTP URI`로 잘 표현된 리소스에 대한 행위를 `HTTP Method`로 정의한다. 리소스의 내용은 json, xml, yaml 등의 다양한 표현 언어로 정의된다.
- `REST`는 기본적으로 웹의 기존 기술과 `HTTP 프로토콜`을 그대로 활용하기 때문에 웹의 장점을 최대한 활용할 수 있는 아키텍처 스타일이다.
- REST는 네트워크 상에서 Client와 Server 사이의 통신 방식 중 하나이다.

### Rest API의 단점

- (보통의 경우) 각각의 자원마다 경로가 따로 있음. 즉, 여러 자원이 동시에 필요한 경우에는 요청을 여러 번 보내야 함 (요청의 횟수 면에서 비효율적)
- (보통의 경우) 자원의 필요한 속성만 얻어올 수 없음. 즉, 일부 속성이 필요하더라도 전체 속성을 가져와야만 함 (요청의 용량 면에서 비효율적)

## GraphQL

GraphQL의 가장 큰 특징 두가지

```
1. GraphQL만의 Schema가 존재한다.
2. 단일 EndPoint
```

- Query : Query는 HTTP의 GET Method와 유사한 작업을 하는 함수다. 즉 Data를 요청하는 함수로, 아래와 같이 사용할 수 있다.

- Mutation : Mutation은 Query와 다르게 생략이 불가능하며, 일반적으로 Data를 수정하는 역할을 진행한다. HTTP와 달리 Delete, Put 등으로 나누지 않고 Mutation 내부에 구현한 함수로 해당 역할을 수행한다. (GET 빼고 나머지 )

expect -> 원하는 테스트
toBe -> 나와야 하는 값

## TDD 개발론이란?

- Test Driven Development : 테스트 주도 개발: 테스트가 개발을 이끌어 나간다.
- 문제를 먼저 정의하고, 문제의 해답을 찾아가는 과정
- 구현 코드가 없는 상황에서 테스트를 먼저 작성해야 한다.

- 만약 어떤 부분에 대한 코딩을 여러번 해봤고 결과가 어떻게 나올지 뻔하다면 TDD를 하지 않아도 된다.

- 고객의 요구조건이 바뀔 수 있는 프로젝트, 개발하는 중에 코드를 많이 바꿔야 된다고 생각하는 경우, 내가 개발하고 나서 이 코드를 누가 유지보수할지 모르는 경우... 즉, 불확실성이 높을 때 TDD를 하면 된다.

## NPM

- Node Package Manager : 자바스크립트 프로그래밍 언어를 위한 패키지 관리자
- 자바스크립트 런타임 환경 Node.js의 기본 패키지 관리자
- Node.js에서 사용가능한 모듈들을 패키지화시켜 모아놓은 것
