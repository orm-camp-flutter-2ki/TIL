실시간으로 생성되고 전송되는 데이터의 흐름

=> 리액티브 프로그래밍

=> 데이터 수정 -> UI 변경이 자동으로

=> 무한

=> 예) 이벤트, 센서 데이터

=> 실시간 분석, 예측, 알림, 감시, 로깅, 모니터링 등에 활용

**StreamBuilder**

- FutureBuilder 와 Future 조합과 비슷
- Stream을 위젯으로 표현하는 위젯
- Future는 단발성이라면 Stream은 지속적은 변화에 따라 화면을 갱신함
- Stream은 센서 데이터 처럼 지속적인 값으로 제공되는 경우가 많음

- Stream 데이터를 UI 로 변환할 필요가 없는 경우에 활용
- listen() 으로 구독
- cancel() 로 해지

listen() 메서드를 통해서 변경을 구독

```dart
_streamController.stream.listen((int number) {
print(number);
1).
```

```dart
StreamSubscription<int>? subscription;
CounterViewModel({
required CounterRepository repository,
}) : _repository = repository {
subscription = _eventController.stream.listen((event) {
print(event);
 });
}
```

listen() 으로 시작한 구독을 해지하려면 StreamSubscription 객체의 인스턴스를 통해야 한다

구독의 해지는 다음 코드로 해야 함

```dart
@override
void dispose() {
subscription?.cancel();
super.dispose();
}
```

StreamController 작성

하나의 리스너를 허용하는 스트림 (Cold Stream)→ 주로 사용

여러 리스너를 허용하는 브로드캐스트 스트림 (Hot Stream)

StreamController의 값 변경

_streamController.add(10); |

add() 메서드를 통해 값을 밀어 넣는다

StreamController 는 값 하나만 가진다.

값이 사용되면 StreamController 에서 제거된다

Stream을 일회성 이벤트에 대해서 스넵바를 띄여주기 위해서 사용하는데

이유는 첫번째는 Streambuilder를 통해서 화면을 그려주는 로직을 사용하고

한번 쓰고 데이터를 비우는 특성을 이용하여 활용해 주기 위해서 사용한다.
