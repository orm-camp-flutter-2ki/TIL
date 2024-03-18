# 제네릭(generic)과 이넘(enum)
## 제네릭(generic)
[매개변수 네이밍](https://dart.dev/effective-dart/design#do-follow-existing-mnemonic-conventions-when-naming-type-parameters)  
- 무엇을 담고 싶은데 타입을 확정하기 어려울 때 타입을 나중에 원하는 형태로 정의할 수 있으며, 타입-안전(type-safe) 효과가 있다.
```dart
class WhatIsInTheBox<T> {
  T? _dataType;

  void put(T data) {
    _data = data;
  }

  T? get() {
    return _data;
  }  
}
```
<br/>

## 이넘(enum)
- 정해둔 값만 넣어둘 수 있는 타입, 이 중에 꺼내써야한다. 휴먼 에러가 줄어든다.
```dart
// enum StateNow 정의
enum StateNow {
  authenticated,
  unauthenticated,
  unknown,
}
```
- `switch` 와 조합해 모든 케이스를 강제적으로 작성하게 한다.  
```dart
  StateNow state = StateNow.unknown;

  switch (state) {
    case StateNow.authenticated:
      print('authenticated');
      break;

    case StateNow.unauthenticated:
      print('unauthenticated');
      break;

    case StateNow.unknown:
      print('unknown');
      break;
  }
```
<br/>

