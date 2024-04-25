240423 (Tue)

플러터 과정 31일차

-----------------
메모
-
**외주** 모든 것은 문서에 남기고 항목 하나하나 세세하게 문서를 작성해야 한다.

항목에 추가 금을 미리 작성해서 알릴 것

[실력 있는 개발자 필요할 땐 | 지엠포컴퍼니](https://greenapps.kr/)

# Stream

실시간으로 생성되고 전송되는 데이터의 흐름

=> 리액티브 프로그래밍

=> 데이터 수정 -> UI 변경이 자동으로

=> 무한

=> 예) 이벤트, 센서 데이터

=> 실시간 분석, 예측, 알림, 감시, 로깅, 모니터링 등에 활용

Dart에서 비슷한 것은 RxDart가 있긴 있다.

StreamBuilder
-

- FutureBuilder 와 Future 조합과 비슷
- Stream을 위젯으로 표현하는 위젯
- Future는 단발성이라면 Stream은 지속적은 변화에 따라 화면을 갱신함
- Stream은 센서 데이터 처럼 지속적인 값으로 제공되는 경우가 많음

구독 / 해지
-

listen() 메서드로 구독 한다.

listen()으로 시작한 구독을 해지 하려면 StreamSubscription 객체의 인스턴스를 통해야한다.

subscription.cancel()

SteamController


```dart
final _streamController = StreamController<int>();
// cold stream => 하나의 리스너를 허용하는 스트림

final _streamController = StreamController<int>.broadcast();
// Hot stream => 여러 리스너를 허용하는 브로드 캐스트스트
```

제네릭 꼭 사용해야한다.
