# 1.3 Asking for Permissions

GeoFencing은 React native 에서는 제공하지 않는 컴포넌트이다. 
React native 에서는 GeoLocation 이라는 것으로 gps 정보를 제공하는데, GeoLocation 은 기능이 몇개 없다. GeoFencing 은 Expo 에서 제공하는 location component 중 하나이다. 만약 사용자가 특정 지역을 이탈하거나 다른 지역에 들어갔을 때 어떻게 하라는 명령을 내릴 수 있게된다.

GeoFencing 을 사용하기  위해선 expo-location 이 추가로 설치가 필요하다.

```
expo install expo-location
```