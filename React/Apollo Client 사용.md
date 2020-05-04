## React App에서 Apollo Client 사용하기

- 참고문서
  https://velog.io/@kim-macbook/using-apollo-client-in-react-app

### Apollo Client를 사용하는 이유

1. REST API와 Redux를 대체하는 GraphQL과 Apollo
1. graphQL을 기반으로 한 상태관리 플랫폼으로 클라이언트에서 테이터를 가져오는게 편리
1. @apollo/react-hooks로 더 간편하게 사용할 수 있다. => useQuery, useMutation, useApolloClient 등
1. 기본적으로 브라우저캐시는 GET 요청만 캐싱하는데 graphQL은 모든 요청을 POST하므로,
   브라우저 캐시를 사용할 수 없기 때문에 Apollo client를 사용한다.
1. 서버에서는 어떠한 자원을 사용할 수 있는지 정의하고, 클라이언트에서 렌더링에 필요한 데이터를 요청하는 방식이다. 꼭 필요한 데이터 교환이 이루어지기 때문에 매우 깔끔하며 효과적이다.

> 🏷 Apollo Client는 GraphQL 기반의 라이브러리로, 클라이언트 애플리케이션의 GraphQL과 데이터 교환을 돕는다. React에서 사용하는 Apollo Client를 특별히 React Apollo라고 부른다.

Apollo Client를 시작하는 가장 간단한 방법은, 권장 설정으로 미리 구성되어있는 스타트 킷(Kit)인 `Apollo-Boost`를 사용하는 것입니다. \
`Apollo-Boost`는 메모리 캐쉬, 로컬 상태 관리 및 오류 처리와 같은 아폴로 앱을 구축하는데 필수적이라고 생각하는 패키지를 포함하고 있습니다. 또한 인증과 같은 기능을 처리할 수 있을 정도로 유연합니다.

### Installation

첫 번째로 몇몇 패키지들을 설치합니다.

`npm install apollo-boost @apollo/react-hooks graphql`\
혹은\
`yarn add apollo-boost @apollo/react-hooks graphql`

- apollo-boost: Apollo Client를 설정하는데 필요한 모든 것이 들어 있는 패키지입니다.
- @apollo/react-hooks: React hooks based view layer integration( React hooks를 위한 apollo)
- graphql: GraphQL 쿼리를 파싱하기 위해 필요한 패키지입니다.

### Create a client

Apollo-boost에서 ApolloClient를 import하시고, GraphQL Server의 엔드포인트를 클라이언트 구성 개체의 uri 프로퍼티에 추가합니다.

```js
import ApolloClient from "apollo-boost";
const client = new ApolloClient({
  uri: "http://localhost:4000",
});
```

### Connect your client to React

Apollo Client를 React에 연결하기 위해 `@apollo/react-hooks`에서 내보낸 `ApolloProvider`컴포넌트를 사용하며 React의 Context.Provider와 비슷합니다.
React App을 감싸고 client를 Context에 배치하여 컴포넌트 트리의 어디에서나 접근할 수 있습니다.

이제 `ApolloProvider`로 React App을 감쌉시다. GraphQL 데이터에 접근해야 하는 어떤 위치보다도 `ApolloProvider`를 App의 가장 높은 곳에 두는 것을 추천합니다.
