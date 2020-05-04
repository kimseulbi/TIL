## Context

Context API를 통해 props를 여러번 가져오거나 또는 상속으로 내려주지 않아도 property들을 가져올수 있습니다.

### 1. createContext

`context.js`

```
// createContext를 import 해줍니다.
import React, { createContext } from "react";

export const AppContext =createContext <AppContextType>({
    // 사실 여기 안에 있는 데이터는 삭제해도 됩니다.
    // 왜냐면 Context.Provider에서 state를 관리합니다.
    // 하지만 관리할 state가 무엇이 있는지 확인하기 좋습니다.
    // 그러기에 지우지 않는것을 추천합니다.

    refreshCount: 0,
    refresh: () => {},
    me: undefined,
    logout: async () => {},
    login: async () => {},
  });
```

### 2. Provider

state를 모아둔 것을 Provider(store)라 생각하면 됩니다.

**export 되는 <ContextProvider>가 하는일**

1. 하위에서 사용 할 state와 setState를 정의합니다.
1. state를 관리할 store를 만들기 위해 creactContext를 받아와서 Context.Provider를 return 합니다.

```js
// 함수같은 것들을 먼저 정의하고
// useState를 통한 state 및 setState를 나중에 했다는 것입니다.

// 사용하고자 하는 컴포넌트 최상위에 지정할 Provider컴포넌트 입니다.
export const AppContextProvider = ({ children }: AppContextProviderProps) => {
  // Hooks를 통한 state, setState를 정의합니다.
  const [client, setClient] = useState<ApolloClient<NormalizedCacheObject>>();
  const [check, setCheck] = useState(false);
  const [me, setMe] = useState<Pro>();
  const [notification, setNotification] = useState<Notification>();
  const [notiListener, setNotiListener] = useState<EventSubscription>();
  const [refreshCount, setRefreshCount] = useState(0);

// 사용할 함수
  const login = async (token: string, me: Pro) => {
    await AsyncStorage.setItem(SAVED_TOKEN_KEY, token);
    // login 시 token을 헤더에 달고, 이동해야 No Authorized 에러가 안뜹니다.
    setClient(initApolloClient(token));
    setMe(me);
  };

  const logout = async () => {
    await AsyncStorage.removeItem(SAVED_TOKEN_KEY);
    // logout 시엔 먼저 토큰을 없애고, 헤더에서 없애야 No Authorized 에러가 안뜹니다.
    setMe(undefined);
    setClient(initApolloClient(undefined));
  };

  const handleNotification = (notification: Notification) => {
    console.log(notification);
    setNotification(notification);
  };

  useEffect(() => {
    setNotiListener(Notifications.addListener(handleNotification));
    // setNotiListener();
    // 2. 스피너가 장착되면 AyncStorage를 통해 스토리지에 token이 저장되어 있는지 확인한다.
    AsyncStorage.getItem(SAVED_TOKEN_KEY).then(async (savedToken) => {
      if (savedToken) {
        try {
          const apolloClient = initApolloClient(savedToken);
          const { data } = await apolloClient.query({
            query: ProMe,
          });
          setCheck(true);
          if (data.proMe) {
            login(savedToken, data.proMe);
          } else {
            logout();
          }
        } catch (error) {
          errHandler(error);
          setCheck(true);
          logout();
        }
      } else {
        setCheck(true);
        logout();
      }
    });
  }, []);

  // 1. client 와 check가 완료될 때까지 기다린다.
  if (!client || !check) return <Loading />;

  // 3. useEffect를 통해 완료가 되면 오류가 나든 안나든 check는 true가 되어서 아래로 간다.
  return (
    // Provider에 state를 사용할 컴포넌트들을 호출하려면
    // {children}이 있어야합니다.
    // 그래서 마지막 return에서 {children}을 리턴해줍니다.
    <AppContext.Provider
      value={{
        refresh: () => setRefreshCount(refreshCount + 1),
        refreshCount,
        me,
        logout,
        login,
      }}
    >
      <ApolloProvider client={client}>{children}</ApolloProvider>
    </AppContext.Provider>
  );
};
```

> **`ApolloProvider`**
>
> `ApolloProvider`는 React의 `Context.Provider`와 비슷합니다. React App을 감싸고 client를 Context에 배치하여 컴포넌트 트리의 어디에서나 접근할 수 있습니다.
>
> GraphQL 데이터에 접근해야 하는 어떤 위치보다도 `ApolloProvider`를 App의 가장 높은곳에 두는 것을 추천합니다. 예를 들어서 React Router를 사용하는 경우, 루트 컴포넌트 외부에 있을 수 있습니다.

### 3. 하위컴포넌트에서 useContext()를 통해 Provider의 state사용

```js
import React from "react";
import { KeyboardAvoidingView, Platform } from "react-native";
// state를 사용하기 위해 앞에서 만든 Provider를 가져옵니다.
import { AppContextProvider } from "./lib/context";
import { SafeAreaProvider } from "react-native-safe-area-context";
import StartScreen from "./screens/StartScreen";

const App = () => {
  return (
    // 사용하고자 하는 자식들 컴포넌트들 가장 밖에서 <Provider>로 감싸줍니다.
    <AppContextProvider>
      <SafeAreaProvider>
        <KeyboardAvoidingView
          style={{ flex: 1 }}
          behavior={Platform.OS === "ios" ? "padding" : undefined}
        >
          <StartScreen />
        </KeyboardAvoidingView>
      </SafeAreaProvider>
    </AppContextProvider>
  );
};

export default App;
```
