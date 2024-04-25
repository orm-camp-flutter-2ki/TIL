# Asynchronous programming: Streams
[공식 문서](https://dart.dev/tutorials/language/streams)


### What's the point?
- Stream은 비동기 데이터 sequence를 제공한다.
- 데이터 sequence에는 사용자가 생성한 event와 파일에서 읽은 데이터가 포함된다.
- Stream API의 `await for`과 listen() 메서드를 통해서 stream을 처리할 수 있다.
- Stream은 에러에 대한 응답(처리) 방법을 제공한다.
- Stream에는 1) 단일 구독(single subscription) 2) 브로드캐스트(broadcast) 2가지가 있다.

Dart에서 비동기 프로그래밍은 크게 Future와 Stream 클래스로 나누어진다.

Future은 즉시 끝나지 않은 연산을 나타낸다. 일반적인 함수가 결과를 반환하는 반면, 비동기 함수는 언젠가 결국 결과를 포함하는(가지는) Future를 반환한다. Future은 결과 값이 준비되면, 이를 알려준다.

Stream은 일련의 비동기 event이다. Stream은 마치 비동기 iterable처럼 보이기도 한다. 다음 event를 요청을 통해 얻지 않고, event가 준비되면 Stream이 이를 알려주는 방식이다.

<br>

## Stream event 수신
Stream은 다양한 방법으로 생성될 수 있다(이는 다른 문서에서 자세히 다룬다). 하지만, 여러 방법으로 생성된 Stream들은 모두 동일한 방법으로 사용된다. `await for`이라고 부르는 비동기 for 반목문을 통해서 Stream의 event를 마치 평범한 for 반복문처럼 다룰 수 있다.
```dart
Future<int> sumStream(Stream<int> stream) async {
  var sum = 0;
  await for (final value in stream) {
    sum += value;
  }
  return sum;
}
```
위의 예제는 정수 event를 단순히 수신하여 더하고 총합을 반환하는 Stream을 보여준다. Stream이 완료되거나 다음 event가 도착하기 전에 반복문의 본문이 종료(수행)되면 함수는 일시중지된다.

`await for` 반복문을 사용하기 위해서는 함수 본문에 async 키워드를 붙여야 한다.

아래의 코드는 async* 함수를 사용해서 단순한 정수 Stream을 생성하여 위의 코드를 테스트한 것이다.
```dart
Future<int> sumStream(Stream<int> stream) async {
  var sum = 0;
  await for (final value in stream) {
    sum += value;
  }
  return sum;
}

Stream<int> countStream(int to) async* {
  for (int i = 1; i <= to; i++) {
    yield i;
  }
}

void main() async {
  var stream = countStream(10);
  var sum = await sumStream(stream);
  print(sum); // 55
}
```

<br>

## Error events
Stream은 event를 더 이상 event가 없는 경우 완료된고 이 event를 수신하는 코드는 Stream에서 새로운 event가 도착했음을 알림받음과 동시에 새로운 event를 수신한다. event를 `await for` 반복문을 통해 읽는 경우, 반복문은 Stream이 완료되면 종료된다.

몇몇 경우에서, Stream이 끝나기 전에 에러가 발생하기도 한다(네트워크 요청 실패, 버그 등 처리해야할 필요가 있는 에러).

Stream은 에러 event 또한 데이터 event를 전달하는 것과 동일하게 전달할 수 있다. 대부분의 Stream은 첫번째 에러 발생 이후에 중지된다. 하지만, Stream은 하나 이상의 에러를 전달할 수도 있고 에러 발생 이후에도 데이터를 계속 전달할 수도 있다. 이 문서에서는 정확히 하나의 에러만을 전달하는 Stream에 대해서만 다룬다.

`await for`를 통해서 Stream을 읽는 경우, 에러는 반복문에 의해 던져(thrown)지고 반복문의 실행은 끝이난다. 발생한 에러는 `try-catch`로 잡을 수 있다.

아래의 코드는 4일 경우 에러를 발생시키는 Stream을 보여준다.
```dart
Future<int> sumStream(Stream<int> stream) async {
  var sum = 0;
  try {
    await for (final value in stream) {
      sum += value;
    }
  } catch (e) {
    return -1;
  }
  return sum;
}

Stream<int> countStream(int to) async* {
  for (int i = 1; i <= to; i++) {
    if (i == 4) {
      throw Exception('Intentional exception');
    } else {
      yield i;
    }
  }
}

void main() async {
  var stream = countStream(10);
  var sum = await sumStream(stream);
  print(sum); // -1
}
```

<br>

## Stream 사용하기
Stream 클래스는 Stream에 대한 일반적인 연산을 제공하는 여러가지 helper 메서드를 포함하고 있다(iterable의 helper 메서드와 유사). 예를 들어, Stream API의 lastWhere() 메서드를 통해 조건을 만족하는 마지막 원소를 얻을 수 있다.
```dart
Future<int> lastPositive(Stream<int> stream) =>
    stream.lastWhere((x) => x >= 0);
```

<br>

## 2종류의 Stream

### Single subscription Stream
가장 일반적인 Stream은 큰 전체의 일부인 일련의 event를 포함하는 형태이다. 이 event들은 정확한 순서로 전달되어야 하고, 어느 것도 놓쳐서는 안된다. 이러한 종류의 Stream은 파일을 읽거나 웹 request를 받을 때 사용된다.

이러한 Stream은 오직 한번만 listen할 수 있다. 최초의 listen 이후에, 다시 listen하는 것은 초기의 event를 놓치는 것고 같고 나머지 Stream event는 의미가 없어진다. 만약 Stream에 대해 listen을 시작했다면, 데이터는 chunk 단위로 읽혀지고 제공된다.

<br>

### Broadcast Stream

다른 종류의 Stream은 각각의 메세지가 한번에 처리되어야 할때 사용된다. 이러한 종류의 Stream은 브라우저에서 마우스 event에 사용된다.

이러한 Stream은 언제든지 listen할 수 있고, listen하는 동안 발행된 event를 수신할 수 있다. 하나 이상의 listenr가 동시에 listen할 수 있고, 이전 구독을 취소하고 동일한 Stream에 대해 다시 listen할 수도 있다.

<br>

## Stream을 반환하는 StreamAPI 메서드
다음의 메서드들은 주어진 Stream에 대한 Stream을 반환한다.
```dart
Future<T> get first;
Future<bool> get isEmpty;
Future<T> get last;
Future<int> get length;
Future<T> get single;
Future<bool> any(bool Function(T element) test);
Future<bool> contains(Object? needle);
Future<E> drain<E>([E? futureValue]);
Future<T> elementAt(int index);
Future<bool> every(bool Function(T element) test);
Future<T> firstWhere(bool Function(T element) test, {T Function()? orElse});
Future<S> fold<S>(S initialValue, S Function(S previous, T element) combine);
Future forEach(void Function(T element) action);
Future<String> join([String separator = '']);
Future<T> lastWhere(bool Function(T element) test, {T Function()? orElse});
Future pipe(StreamConsumer<T> streamConsumer);
Future<T> reduce(T Function(T previous, T element) combine);
Future<T> singleWhere(bool Function(T element) test, {T Function()? orElse});
Future<List<T>> toList();
Future<Set<T>> toSet();
```
drain()과 pipe() 함수를 제외한 모든 함수들은 iterable의 동일한 이름의 메서드와 비슷하게 동작한다. 각각의 함수들은 async 함수 내부의 `await for` 반복문을 통해 쉽게 구현할 수 있다.  

아래는 직접 구현한 예시 (실제 메서드는 좀 더 복잡함)
```dart
Future<bool> contains(Object? needle) async {
  await for (final event in this) {
    if (event == needle) return true;
  }
  return false;
}

Future forEach(void Function(T element) action) async {
  await for (final event in this) {
    action(event);
  }
}

Future<List<T>> toList() async {
  final result = <T>[];
  await forEach(result.add);
  return result;
}

Future<String> join([String separator = '']) async =>
    (await toList()).join(separator);
```

<br>

## Stream을 조작하는 메서드
다음의 메서드들은 주어진 Stream에 대한 새로운 Stream을 반환한다. 각각의 메서드들은 원본 Stream을 listen하기 전에 새로운 Stream에 listener가 생기기 전까지 기다린다.
```dart
Stream<R> cast<R>();
Stream<S> expand<S>(Iterable<S> Function(T element) convert);
Stream<S> map<S>(S Function(T event) convert);
Stream<T> skip(int count);
Stream<T> skipWhile(bool Function(T element) test);
Stream<T> take(int count);
Stream<T> takeWhile(bool Function(T element) test);
Stream<T> where(bool Function(T event) test);
```
위의 메서드들은 =iterable의 동일한 이름의 (iterable을 다른 iterable로 변형하는)메서드와 비슷하게 동작한다. 각각의 함수들은 async 함수 내부의 `await for` 반복문을 통해 쉽게 구현할 수 있다.  

아래는 직접 구현한 예시
```dart
Stream<E> asyncExpand<E>(Stream<E>? Function(T event) convert);
Stream<E> asyncMap<E>(FutureOr<E> Function(T event) convert);
Stream<T> distinct([bool Function(T previous, T next)? equals]);
```
asyncExapnd()와 asyncMap() 함수들은 exapnd()와 Map()함수와 비슷하다. 하지만 자신의 인자로 받는 함수들이 비동기(async) 함수인 것을 허용한다. distinct() 함수는 Iterable에는 없지만, Stream에는 존재한다. 
```dart
Stream<T> handleError(Function onError, {bool Function(dynamic error)? test});
Stream<T> timeout(Duration timeLimit,
    {void Function(EventSink<T> sink)? onTimeout});
Stream<S> transform<S>(StreamTransformer<T, S> streamTransformer);
```
위의 3 함수들은 좀더 특별하다. 이들은 `await for` 반복문이 수행할 수 없는 에러(한번 발생하면 반복문과 Stream에 대한 구독을 중지시키는 에러)를 핸들링할 수 있는 기능을 포함한다. 이러한 에러를 복구하는 방법은 없다. 아래의 코드는 handleError() 메서드가 `await for` 반복문에서 에러를 사용하기 전에, 어떻게 Stream에서 에러를 제거하는지 보여준다.
```dart
Stream<S> mapLogErrors<S, T>(
  Stream<T> stream,
  S Function(T event) convert,
) async* {
  var streamWithoutErrors = stream.handleError((e) => log(e));
  await for (final event in streamWithoutErrors) {
    yield convert(event);
  }
}
```

<br>

### transform() 함수
transfrom() 함수는 에러 핸들링만을 위한 것은 아니다. transform()은 Stream에서 보다 일반적인 map() 함수이다. 보통 map() 함수는 각각의 event당 하나의 값을 요구한다. 하지만 특히 I/O Stream은 몇몇의 입력 event에 대해 하나의 output event를 생성하기도 한다. StreamTransformer는 이러한 처리에 유용하다. 예를 들어, Utf8Decoder과 같은 decoder는 transformer이다. transformer는 bind()라는 하나의 함수만을 인자로 갖고, bind() 함수는 async 함수를 통해 쉽게 구현할 수 있다.

<br>

### File 읽고 decode하기
아래의 코드는 파일을 읽고 2개의 transform을 Stream에 실행하는 예제이다. 첫번째는 UTF8로부터 데이터를 변환하고, 이 후 LineSplitter를 실행한다. 해시태그를 제외한 모든 줄을 출력한다.
```dart
import 'dart:convert';
import 'dart:io';

void main(List<String> args) async {
  var file = File(args[0]);
  var lines = utf8.decoder
      .bind(file.openRead())
      .transform(const LineSplitter());
  await for (final line in lines) {
    if (!line.startsWith('#')) print(line);
  }
}
```

<br>

## listen() 메서드
Stream의 마지막 메서드는 listen()이다. 이는 'low-level' 메서드로 모든 Stream 함수들은 listen()에 대해(최종 수신이므로) 작성된다.
```dart
StreamSubscription<T> listen(void Function(T event)? onData,
    {Function? onError, void Function()? onDone, bool? cancelOnError});
```
새로운 Stream 타입을 생성하기 위해서는 Stream 클래스를 extend하고, listen() 메서드를 구현하면 된다. (Stream의 다른 모든 메서드들은 동작을 위해 listen()을 호출한다.)

listen() 메서드는 Stream에 대한 listen을 시작하도록 한다. Stream에 대해 listen하는 동안에는 수신하기를 원하는 나타내는 비활성 객체이다. Stream을 listen하면 event를 생산하는 동작중인 Stream을 나타내는 StreamSubscription 객체가 반환된다. 이는 Iterable이 단지 객체의 모음일 뿐이지만, iterator이 실제 반복을 수행하는 객체인지와 유사하다.

Stream에 대한 구독은 일시정지, 일시정지 후 다시 구독, 완전히 취소가 가능하다. 또한, 각각의 데이터 event, 에러 event, 혹은 Stream이 닫히는 경우에 호출될 콜백을 지정할 수도 있다.


