# One Line Diary Boilerplate(CRUD)

## CREATE
* input창에 text를 입력받는다.
    * 빈칸 입력시 alert 트리거.
* 입력을 받은 후 확인버튼 클릭& 엔터.
    * 입력받은 데이터 POST방식으로 보낸다.
        * 각 DATA에 ID 지정
        * READ를 통해 최신 일기 불러오기.

## READ
* 데이터를 가져와 출력시킨다.
    * 데이터가 없을때 일기를 쓰도록 제안하는 텍스트 형태의 DOM을 그려준다.

## UPDATE
* 수정 버튼 제공하여 클릭시 별도의 인풋 제공
    * 수정 내용 입력후 엔터 이벤트를 && 수정 확인 버튼 제공
        * 데이터 등록
    * 고유한 DOM 탐색하여 입력된 데이터 등록
    * 취소버튼 제공
        * 별도의 인풋 DOM 제거
* 취소버튼 제공

## DELETE
* 삭제 버튼 클릭시 삭제



## 참고사항 

1. export default 축약 - 한개만 내보냄 (export default)
1. parameter === []
1. payload가 어떻게 쓰이는지 알아야함 
```js
const payload = {
    id: input,
    date: this.nowDate()
}
```
1. 두개이상이면 객체로 사용 
1. 한곳에서만 사용한다면 패키지화 한다. 
```js
        let year = date.getFullYear(),
         month = date.getMonth() + 1,
         day = date.getDate(),
         hour = date.getHours(),
         minutes = date.getMinutes(),
         seconds = date.getSeconds(),
         ampm = hour >= 12 ? 'pm' : 'am';
```
1. CustomEvent 
1. this최소화 
1. error log 
1. get,set 사용 
