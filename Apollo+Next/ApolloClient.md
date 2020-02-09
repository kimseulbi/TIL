#ApolloClient

### Apollo Client를 사용한 컴포넌트 렌더링
Apollo Client는 GraphQL 기반의 라이브러리로, 클라이언트 애플리케이션의 GraphQL과 데이터 교환을 돕는다. React에서 사용하는 Apollo Client를 `React Apollo`라고 부릅니다. 

GraphQL은 서버 API를 통해 정보를 주고받기 위해 사용하는 질의 언어이다. GraphQL API는 보통 하나의 엔드포인트를 사용 하며, 요청시 사용하는 질의문에 따라 응답의 구조가 달라진다. 

![](https://cdn-images-1.medium.com/max/1600/1*qpyJSVVPkd5c6ItMmivnYg.png)

<Card/> 컴포넌트 렌더링에 필요한 데이터를 GraphQL을 사용해 가져오는 쿼리는 다음 예와 같이 작성한다. 
```js
 query Card($id: Float!) { // Operation type  
  match(id: $id) {        // Operation "endpoint"
    card {
      title               // Requested fields
      body
    }
  }
}
```
위와 같이 하면 <Card/> 컴포넌트에 필요한 데이터를 prop와 연결해 서버에서 받아온다. 위 코드에서는 컴포넌트 렌더링에 필요한 데이터에만 집중하고 있다. 

질의 문으로 실행할 수 있는 작업 유형은 다음과 같다. 

![](https://d2.naver.com/content/images/2019/06/helloworld-201903-seungho-3.png)

* query: 데이터를 받아올 때 사용한다. 
* mutation: 데이터를 생성, 수정, 삭제할 때 사용한다. HTTP와 달리 Delete, Put 등으로 나누지 않고 mutation 내부에 구현한 함수로 해당 역활을 수행한다.
* subscription: 웹 소켓을 사용해 실시간 양방향 통신을 구현할 때 사용한다.

### Apollo Client 적용 예시

GraphQL 쿼리는 Apollo Client에서 컴포넌트와 함께 사용할 수 있다. 다음은 react-apollo의 <Query/> 컴포넌트를 사용해 서버에서 받은 데이터를 화면에 보여 주는 코드의 예입니다.  

```js
import gql from "graphql-tag";  
import { Query } from "react-apollo";

const GET_DOGS = gql`  
  {
    dogs {
      id
      breed
    }
  }
`;

const Dogs = ({ onDogSelected }) => (  
  <Query query={GET_DOGS}>
    {({ loading, error, data }) => {
      if (loading) return "Loading...";
      if (error) return `Error! ${error.message}`;

      return (
        <select name="dog" onChange={onDogSelected}>
          {data.dogs.map(dog => (
            <option key={dog.id} value={dog.breed}>
              {dog.breed}
            </option>
          ))}
        </select>
      );
    }}
  </Query>
);
```

컴포넌트 사용에 필요한 GrapgQL 쿼리의 문자열은 qql 함수로 감싸야 한다. qql 함수호 감싼 GraphQL 쿼리를 <>

출처: [Apollo Client는 Redux와 무엇이 다른가](https://d2.naver.com/helloworld/4245995)



