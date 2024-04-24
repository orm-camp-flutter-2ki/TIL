## Stream
실시간으로 생성되고 전송되는 데이터의 흐름
실시간 분석, 예측, 알림, 감시, 로깅, 모니터링 등에 활용

## Stream 활용 방법
* StreamBuilder
* 구독/해지

<br></br>

## StreamBuilder
#### ✔️ Stream 데이터를 UI로 변환해주는 위젯
* FutureBuilder와 Future 조합과 비슷
* Stream을 위젯으로 표현하는 위젯
* Future는 단발성이라면 Stream은 지속적인 변화에 따라 화면을 갱신한다.

<img width="436" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/e3afc81f-b78c-46a4-bcb8-40f193a07bcd">

<br></br>

## 구독과 해지
#### ✔️ Stream 데이터를 UI로 변환할 필요가 없는 경우에 활용
* stream을 제어하는 도구 중 하나
* listen()으로 구독, cancel()로 해지

### StreamController 작성
* 하나의 listener를 허용하는 stream(cold stream)
<img width="499" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/d693698e-51e7-4657-8698-2ba2ea272a8d">

* 하나의 listener를 두 번이상 시도하려고 하면 에러 발생
* => 여러 listener를 사용하려면 broadcast stream 사용(hot stream)
<img width="619" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/5a5f2483-1066-4301-8b42-92b09496bfdf">

#### 예시 코드
```dart
import 'dart:async';

void main() async {
  // stream 생성
  final streamController = StreamController<int>();

  // stream 의 이벤트를 구독하여 데이터 수신
  final StreamSubscription<int> subscription =
      streamController.stream.listen((event) {
    print('Received data: $event');
  });

  // stream 에서 데이터 전송
  streamController.sink.add(1);
  streamController.sink.add(2);
  streamController.sink.add(3);

  // stream 종료
  streamController.close();
}

```

* listen() 메서드를 통해 데이터 변경을 구독한다.
* add() 메서드를 통해 값을 넣는다.
  * StreamController는 값 하나만 가진다.
  * 값이 사용되면 StreamController에서 제거된다.
* StreamSubscription 객체의 인스턴스를 통해 `streamController.stream.listen()` 메서드를 통한 구독을 취소한다.
<img width="350" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/a607b9bb-7947-460d-8492-1c9797f48035">

* `streamController.close()` 메서드는 Stream을 완전히 종료한다.
  * Stream이 닫히면 더 이상 새로운 데이터를 추가할 수 없다.
  * Stream을 다시 사용하려면 새로운 StreamController를 생성해야 한다.

<img width="631" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/b4c48745-3350-4752-af5e-7167e2748992">

* sink는 스트림에 데이터를 넣어주는 역할을 하며, steam은 데이터 파이프를 타고 넘어오는 데이터를 꺼내는데 사용한다.
  * `streamController.sink.add()`로 넣고
  * `streamController.stream.listen()`로 꺼낸다.

### Stream을 활용한 일회성 UI 이벤트 처리 방법 예시
* Stream이 노출하는 값은 일회성이기 때문에 단발성 UI 처리에 활용할 수 있다.
  * SnackBar, 다이얼로그 표시 등
* 각 화면에서 발생하는 UI 이벤트를 Sealed 클래스로 정의하여 모든 이벤트 처리를 강제한다.

<img width="600" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/850ca9a0-f062-441c-8399-e51d2fd8790f">
<img width="534" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/aba8f972-72e9-4d52-8d5b-2969d552688a">


### StreamController.add와 sink.add의 차이점
<img width="650" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/5fa1c725-b397-4a34-8cf8-9f8c5c11951c">

#### ✔️ streamController.add()
* StreamController는 Stream과 Sink 두 가지 역할을 한다.
* add() 메서드는 Stream과 Sink 모두에 데이터를 추가한다.
* 이 경우 streamController.add를 호출하면 내부적으로 sink.add가 호출되어 데이터가 Stream에 전달된다.

#### ✔️ streamController.sink.add()
* streamController.sink는 StreamSink의 인터페이스로 객체로 sink의 기능들만 사용할 수 있게 된다.
  * 명시적으로 sink을 사용하여 데이터를 Stream에 추가하는 것이다.

<br></br>

## 기타
* StreamController 뒤에 <> 제네릭을 반드시 작성해 준다.
* 생성자 안에서는 asncy를 사용하지 못하기 때문에 필요하다면 then()을 사용한다.
* `flutter pub add (package 이름) —dev` 명령어로 dev dependency에 패키지를 추가할 수 있다.
* Provider의 watch()는 buid() 생성 부분에서만, read()는 init, 이벤트 발생할 때 사용한다.
