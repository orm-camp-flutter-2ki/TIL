## Debounce와 Throttle
* Debounce와 Throttle 모두 특정 함수의 실행을 제한한다.
* 무한 스크롤, 타이핑, 연속된 클릭과 같이 연속적으로 발생한 이벤트를 하나로 처리하는 방식이다.
* 호출 할 로직이 거대할 경우 혹은 유료 API를 호출 해야 하는 경우 성능 저하, 과도한 요금 청구를 막을 때도 사용된다.

<img width="721" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/ac3efae7-4947-4397-95c2-fa5b7eede056">

<br></br>

## Debounce
* Debounce는 특정 기간 안의 함수 실행을 모두 취소하고 마지막에만 실행한다.
* 지정해놓은 시간 동안 다시 함수가 재호출되면 기존의 함수를 취소하고 재호출된 함수를 지정해놓은 시간 동안 기다리고 실행한다.
* 예시: 키워드 검색 혹은 자동완성 기능에서 api 함수 호출 횟수를 최대한 줄이고 싶을 때

<img width="698" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/f7596ad9-ce26-4a85-9dfb-fc58b8791748">

<br></br>

## Throttle 
* Throttle은 함수 실행 후 특정 기간 동안의 추가 실행을 모두 취소한다.
* 스크롤, 버튼 클릭을 통해서 요청을 보내거나, 다음 화면으로 이동하는 경우에는 쓰로틀링이 적합하다.
* 화면 이동 전에 버튼을 두 번 터치할 수 있어서 화면이 중첩되는 앱이 실제로도 많다.

<img width="787" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/1daba568-99c5-453a-bfac-487be914f22c">

📝 [선생님 코드](https://github.com/orm-camp-flutter-2ki/learn_flutter_together/blob/master/lib/08_debounce/presentation/search_list/search_list_view_model.dart)  
📝 [블로그](https://velog.io/@sht-3756/Debounce와Throttle사용)



