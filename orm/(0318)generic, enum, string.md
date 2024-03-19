## 1. 제네릭(Generic)
* 타입을 나중에 원하는 형태로 정의할 수 있다.
* 타입 안전(type safe) 효과
* 사용 예시
<img width="299" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/a5604a34-e809-4825-a78d-20086a467b91">

* 이용 가능한 타입에 제약을 추가한 경우
<img width="324" alt="image" src="https://github.com/NalaJang/TIL/assets/73895803/80b1f8bd-ad30-49cc-a857-60081dcb0ffd">

<br></br>

## 2. 열거형(Enum)
* 정해둔 값만 넣어둘 수 있는 타입(키 타입을 정의하는 것)
* switch 와의 조합으로 모든 케이스를 강제로 작성해야 한다.

```dart
enum AuthState {
  authenticated,
  unauthenticated,
  unknow,
}
```

```dart
AuthState authState = AuthState.unknown;

// ...

switch(authState) {
  case AuthState.authenticated:
    print('authenticated');
    break;
  
  case AuthState.unauthenticated:
    print('unauthenticated');
    break;
  
  case AuthState.unknown:
    print('unknown');
    break;
}
```

<br></br>

## 3. 문자열
### 3.1. 문자열 처리

```dart
const String hello = 'HELLO';

  // 일부 떼어내기
  print(hello.substring(0,2)); // 출력 결과: HE

  // 일부 치환
  print(hello.replaceAll('LL', 'GG')); // 출력 결과: HEGGO

  // 분리
  final number = '1,2,3';
  final splited = number.split(',');
  splited.forEach((element) {
    print(element);
  });
  // 출력 결과
  // 1
  // 2
  // 3

  // 검색
  print(hello.indexOf('E')); // 출력 결과 : 1
  print(hello.contains('O')); // 출력 결과 : true
```

### 3.2. 문자열 결합 방법
* `+`
* stirngInterpolation
* stringBuffer

### stringBuffer
* write() 메서드로 결합한 결과를 내부 메모리(버퍼)에 담아두고 toString()으로 결과를 얻음

```dart
final buffer = StringBuffer('Dart');
buffer..write(' and ')
..write('Flutter');

print(buffer.toString()); // 출력 결과 : Dart and Flutter
```

> .. (cascade) 연산자 : void 리턴인 함수의 앞에 사용하면 해당 객체의 레퍼런스를 반환하여 메서드 체인을 사용할 수 있음

### `+` 연산자가 느린 이유
`String`은 불변 객체(immutable)이기 때문에 생성될 때마다 `new`로 생성되기 때문이다.

<br></br>

## 4. 기타
### Switch statements의 Switch expressions
* switch 문을 아래처럼 작성도 가능하다.
* `식` 처럼 사용해서 값이 리턴되는 형태

```dart
var x = switch (y) { ... };

print(switch (x) { ... });

return switch (x) { ... };
```

* 오늘 연습 문제에도 적용해 보았다.
```dart

// 적용하기 전
String? get() {
  usageCount++;

  switch (keyType) {
    case KeyType.padlock:
      if (usageCount <= padlockUsageValue) {
        return null;
      }
    case KeyType.button:
      if (usageCount <= buttonUsageValue) {
        return null;
      }
    case KeyType.dial:
      if (usageCount <= dialUsageValue) {
        return null;
      }
    case KeyType.finger:
      if (usageCount <= fingerUsageValue) {
        return null;
      }
  }
```

```dart
// 적용 후
T? get() {
  _usageCount++;

  var limitCount =
  switch(_keyType) {
    KeyType.padlock => padlockUsageValue,
    KeyType.button => buttonUsageValue,
    KeyType.dial => dialUsageValue,
    KeyType.finger => fingerUsageValue,
  };

  return _usageCount < limitCount ? null : _data;
}
```

[참고][Dart switch statements](https://dart.dev/language/branches#switch-expressions)

### Test 할 때는 모든 경우를 테스트 하는 것이 좋다.
