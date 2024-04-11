# Asynchrony support
[공식문서](https://dart.dev/language/async) 

Dart 라이브러리에는 Future, Stream 객체를 반환하는 함수들이 많다. 이러한 함수들은 시간이 많이 걸리는 작업(I/O와 같은)을 수행하는 동안 작업이 완료되기를 기다리지 않고, 결과 객체를 반환하기에 비동기적(asynchronous)이라고 한다.  

async와 await 키워드를 통해 비동기 프로그래밍을 지원한다.

<br>

## Futures 사용법
완료된(실제 연산의 결과의 값이 반환된) Future이 필요한 경우 2가지 선택지가 있다.  
1. aync, await 사용
2. Future API 사용

await는 반드시 async로 표시된 함수 내부에서만 사용할 수 있다.  
```dart
Future<void> checkVersion() async {
  var version = await lookUpVersion();
  // Do something with version
}
```
=> async 함수는 시간이 많이 소요되는 작업이긴 하지만 작업이 끝날 때까지 기다리진 않고, async 함수 내부의 await 표현식을 만나기 전까지만 실행된다. awiat 표현식을 만나면 Future 객체를 일단 반환하고,  await 표현식이 완료되면 다시 재개된다.

await 키워드는 async 함수 내부에서 여러번 호출될 수도 있다.

await 표현식 내부에서 표현식의 값은 항상 Future이다. Future이 아니어도 Future로 자동으로 래핑된다. Future 객체는 이 후에 실제 객체(값)를 반환할 것을 보장함을 뜻한다. await 표현식은 그 결과 객체(값)가 사용가능해 질때까지 실행을 일시중지 하기 때문에, await 표현식의 반환 값은 항상 실제 객체(값)이다.

<br>

## async functions 선언

async 함수는 async 변경자로 표시된 본문 블럭을 가진 함수를 뜻한다.  

함수에 async 키워드를 붙이면 반환 타입이 Future가 된다.  

아래와 같이 String을 반환하는 함수에 async 키워드를 붙이면 반환 타입이 Future\<String\>이 된다.  
`Future<String> lookUpVersion() async => '1.0.0';`  

Future 객체가 필요한 경우, Dart가 알아서 Future 객체를 만들어 주기 때문에, 함수 본문에서 Future API를 사용할 필요가 없다. 만약, 아무것도 반환하지 않는 함수를 만들고 싶다면, 반환 타입을 Future\<void\>로 하면 된다.

<br>

## Stream 사용법

Stream에서 값을 얻어야 한다면 2가지 선택지가 있다.
1. async 키워드와 비동기 for loop(await for)을 사용한다.
2. Stream API를 사용한다.

=> await for를 사용하기 전에, 정말 모든 stream의 결과를 기다리기를 원하는 것인지, awiat for가 코드를 더 깔끔하게 하는 것인지 확인하여야 한다. 예를 들어, UI 프레임워크는 이벤트에 대한 끝이 없는 stream을 보내기 때문에 UI 이벤트 리스너에 await for를 사용해서는 안된다.

비동기 for loop는 아래와 같은 형태이다.
```dart
await for (varOrType identifier in expression) {
  // Executes each time the stream emits a value.
}
```

표현식의 값은 반드시 Stream 타입이어야한다. 
동작 과정은 아래와 같다.
1. stream이 값을 emit할 때까지 기다린다.
2. emit된 값으로 설정된 변수와 함께 for loop의 본문을 실행한다.
3. 1, 2의 과정을 stream이 닫힐 때까지 반복한다.

stream으로 부터 값을 받아오는 것을 멈추려면, break나 return을 사용하여, for loop의 실행을 중지하고 stream 감지를 중단하면 된다.

만약 비동기 for loop를 구현하는 중에 컴파일에러가 발생하였다면, async 함수 내부에 await for가 사용되고 있는지 확인해라. 예를 들어, 비동기 for loop를 앱의 main 함수에서 사용하는 경우 main 함수는 async여야 한다.
